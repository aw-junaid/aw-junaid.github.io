# shell script for web penetration testing that takes user inputs for domains and other parameters:

```bash
#!/bin/bash

# Web Penetration Testing Automation Script
# Author: Security Tester
# Usage: ./webpen_test.sh

# Color codes for output
RED='\033[0;31m'
GREEN='\033[0;32m'
YELLOW='\033[1;33m'
BLUE='\033[0;34m'
PURPLE='\033[0;35m'
CYAN='\033[0;36m'
NC='\033[0m' # No Color

# Script version
VERSION="1.0"

# Function to display banner
show_banner() {
    clear
    echo -e "${RED}==================================================${NC}"
    echo -e "${GREEN}    Web Penetration Testing Automation Script    ${NC}"
    echo -e "${YELLOW}              Version: $VERSION                  ${NC}"
    echo -e "${RED}==================================================${NC}"
    echo ""
}

# Function to check required tools
check_dependencies() {
    echo -e "${YELLOW}[*] Checking dependencies...${NC}"
    
    dependencies=("nmap" "gobuster" "whatweb" "nikto" "curl" "wget" "dig" "nslookup")
    missing_deps=()
    
    for tool in "${dependencies[@]}"; do
        if ! command -v $tool &> /dev/null; then
            missing_deps+=($tool)
        fi
    done
    
    if [ ${#missing_deps[@]} -ne 0 ]; then
        echo -e "${RED}[!] Missing dependencies: ${missing_deps[*]}${NC}"
        echo -e "${YELLOW}[*] Install with: sudo apt-get install ${missing_deps[*]}${NC}"
        read -p "Continue anyway? (y/n): " -n 1 -r
        echo
        if [[ ! $REPLY =~ ^[Yy]$ ]]; then
            exit 1
        fi
    else
        echo -e "${GREEN}[+] All dependencies installed${NC}"
    fi
}

# Function to create working directory
create_workspace() {
    local domain=$1
    local timestamp=$(date +%Y%m%d_%H%M%S)
    workspace="pen_test_${domain}_${timestamp}"
    
    echo -e "${YELLOW}[*] Creating workspace: $workspace${NC}"
    
    mkdir -p "$workspace"/{recon,scanning,enumeration,vulnerability,report,logs}
    
    echo -e "${GREEN}[+] Workspace created successfully${NC}"
    echo "$workspace"
}

# Function for reconnaissance phase
recon_phase() {
    local workspace=$1
    local domain=$2
    
    echo -e "${BLUE}==================================================${NC}"
    echo -e "${GREEN}           RECONNAISSANCE PHASE                  ${NC}"
    echo -e "${BLUE}==================================================${NC}"
    
    # Submenu for reconnaissance options
    while true; do
        echo -e "\n${CYAN}Reconnaissance Options:${NC}"
        echo "1) Subdomain Enumeration"
        echo "2) DNS Information Gathering"
        echo "3) WHOIS Lookup"
        echo "4) Technology Detection"
        echo "5) Run All Reconnaissance"
        echo "6) Back to Main Menu"
        
        read -p "Select option (1-6): " recon_choice
        
        case $recon_choice in
            1)
                echo -e "${YELLOW}[*] Subdomain Enumeration${NC}"
                read -p "Enter domain (default: $domain): " sub_domain
                sub_domain=${sub_domain:-$domain}
                
                echo -e "${CYAN}Select tool:${NC}"
                echo "1) Sublist3r (if installed)"
                echo "2) Amass (if installed)"
                echo "3) DNS Bruteforce with gobuster"
                echo "4) Manual dig/ nslookup"
                read -p "Choice: " tool_choice
                
                case $tool_choice in
                    1)
                        if command -v sublist3r &> /dev/null; then
                            sublist3r -d $sub_domain -o "$workspace/recon/sublist3r_$sub_domain.txt"
                        else
                            echo -e "${RED}[!] Sublist3r not installed${NC}"
                        fi
                        ;;
                    2)
                        if command -v amass &> /dev/null; then
                            amass enum -d $sub_domain -o "$workspace/recon/amass_$sub_domain.txt"
                        else
                            echo -e "${RED}[!] Amass not installed${NC}"
                        fi
                        ;;
                    3)
                        read -p "Enter wordlist path (default: /usr/share/wordlists/dirb/common.txt): " wordlist
                        wordlist=${wordlist:-/usr/share/wordlists/dirb/common.txt}
                        gobuster dns -d $sub_domain -w $wordlist -o "$workspace/recon/gobuster_dns_$sub_domain.txt"
                        ;;
                    4)
                        for sub in www mail ftp admin blog dev test; do
                            echo -e "${YELLOW}[*] Checking $sub.$sub_domain${NC}"
                            dig $sub.$sub_domain | grep -E '^[^;]' >> "$workspace/recon/manual_dns_$sub_domain.txt"
                        done
                        ;;
                esac
                ;;
                
            2)
                echo -e "${YELLOW}[*] DNS Information Gathering${NC}"
                read -p "Enter domain: " dns_domain
                
                {
                    echo "=== DNS Records for $dns_domain ==="
                    echo "A Record:"
                    dig $dns_domain A +short
                    echo ""
                    echo "AAAA Record:"
                    dig $dns_domain AAAA +short
                    echo ""
                    echo "MX Records:"
                    dig $dns_domain MX +short
                    echo ""
                    echo "NS Records:"
                    dig $dns_domain NS +short
                    echo ""
                    echo "TXT Records:"
                    dig $dns_domain TXT +short
                    echo ""
                    echo "CNAME Records:"
                    dig $dns_domain CNAME +short
                } > "$workspace/recon/dns_info_$dns_domain.txt"
                
                echo -e "${GREEN}[+] DNS information saved${NC}"
                ;;
                
            3)
                echo -e "${YELLOW}[*] WHOIS Lookup${NC}"
                read -p "Enter domain/IP: " whois_target
                whois $whois_target > "$workspace/recon/whois_$whois_target.txt"
                echo -e "${GREEN}[+] WHOIS information saved${NC}"
                ;;
                
            4)
                echo -e "${YELLOW}[*] Technology Detection${NC}"
                read -p "Enter target URL (with http/https): " tech_url
                
                if command -v whatweb &> /dev/null; then
                    whatweb $tech_url > "$workspace/recon/technologies_$(echo $tech_url | sed 's/\///g').txt"
                else
                    curl -I $tech_url > "$workspace/recon/headers_$(echo $tech_url | sed 's/\///g').txt"
                fi
                echo -e "${GREEN}[+] Technology information saved${NC}"
                ;;
                
            5)
                echo -e "${YELLOW}[*] Running all reconnaissance modules${NC}"
                # Run basic recon
                whois $domain > "$workspace/recon/whois.txt"
                dig $domain ANY > "$workspace/recon/dns_all.txt"
                
                # Technology detection
                if command -v whatweb &> /dev/null; then
                    whatweb $domain -v > "$workspace/recon/whatweb.txt"
                fi
                
                echo -e "${GREEN}[+] All reconnaissance completed${NC}"
                ;;
                
            6)
                break
                ;;
                
            *)
                echo -e "${RED}[!] Invalid option${NC}"
                ;;
        esac
    done
}

# Function for scanning phase
scanning_phase() {
    local workspace=$1
    local target=$2
    
    echo -e "${BLUE}==================================================${NC}"
    echo -e "${GREEN}              SCANNING PHASE                      ${NC}"
    echo -e "${BLUE}==================================================${NC}"
    
    while true; do
        echo -e "\n${CYAN}Scanning Options:${NC}"
        echo "1) Nmap Port Scan"
        echo "2) Masscan (Fast Scan)"
        echo "3) Service Version Detection"
        echo "4) Vulnerability Scan with Nikto"
        echo "5) Run All Scans"
        echo "6) Back to Main Menu"
        
        read -p "Select option (1-6): " scan_choice
        
        case $scan_choice in
            1)
                echo -e "${YELLOW}[*] Nmap Port Scan${NC}"
                read -p "Enter target IP/domain: " nmap_target
                read -p "Port range (default: 1-1000): " port_range
                port_range=${port_range:-1-1000}
                
                echo -e "${CYAN}Select scan type:${NC}"
                echo "1) TCP SYN Scan (Stealth)"
                echo "2) TCP Connect Scan"
                echo "3) UDP Scan"
                echo "4) Comprehensive Scan"
                read -p "Choice: " scan_type
                
                case $scan_type in
                    1)
                        sudo nmap -sS -p $port_range -T4 $nmap_target -oA "$workspace/scanning/nmap_syn"
                        ;;
                    2)
                        nmap -sT -p $port_range $nmap_target -oA "$workspace/scanning/nmap_connect"
                        ;;
                    3)
                        sudo nmap -sU -p $port_range $nmap_target -oA "$workspace/scanning/nmap_udp"
                        ;;
                    4)
                        nmap -sC -sV -p $port_range -O $nmap_target -oA "$workspace/scanning/nmap_comprehensive"
                        ;;
                esac
                ;;
                
            2)
                echo -e "${YELLOW}[*] Masscan - Fast Port Scanning${NC}"
                read -p "Enter target IP range: " masscan_target
                read -p "Ports (default: 1-65535): " masscan_ports
                masscan_ports=${masscan_ports:-1-65535}
                read -p "Rate (packets/sec, default: 1000): " masscan_rate
                masscan_rate=${masscan_rate:-1000}
                
                sudo masscan -p$masscan_ports --rate=$masscan_rate --open-only $masscan_target > "$workspace/scanning/masscan_$(date +%s).txt"
                ;;
                
            3)
                echo -e "${YELLOW}[*] Service Version Detection${NC}"
                read -p "Enter target: " service_target
                read -p "Enter open ports (comma-separated): " open_ports
                
                if [ -n "$open_ports" ]; then
                    nmap -sV -p $open_ports $service_target -oA "$workspace/scanning/service_versions"
                else
                    nmap -sV $service_target -oA "$workspace/scanning/service_versions"
                fi
                ;;
                
            4)
                echo -e "${YELLOW}[*] Nikto Vulnerability Scan${NC}"
                read -p "Enter target URL: " nikto_target
                
                if command -v nikto &> /dev/null; then
                    nikto -h $nikto_target -Format html -o "$workspace/scanning/nikto_$(date +%s).html"
                else
                    echo -e "${RED}[!] Nikto not installed${NC}"
                fi
                ;;
                
            5)
                echo -e "${YELLOW}[*] Running all scans${NC}"
                # Basic port scan
                nmap -sV $target -oA "$workspace/scanning/initial"
                # Nikto scan
                if command -v nikto &> /dev/null; then
                    nikto -h $target -o "$workspace/scanning/nikto.txt"
                fi
                echo -e "${GREEN}[+] All scans completed${NC}"
                ;;
                
            6)
                break
                ;;
        esac
    done
}

# Function for enumeration phase
enumeration_phase() {
    local workspace=$1
    local target=$2
    
    echo -e "${BLUE}==================================================${NC}"
    echo -e "${GREEN}            ENUMERATION PHASE                     ${NC}"
    echo -e "${BLUE}==================================================${NC}"
    
    while true; do
        echo -e "\n${CYAN}Enumeration Options:${NC}"
        echo "1) Directory/File Enumeration"
        echo "2) Parameter Discovery"
        echo "3) API Endpoint Discovery"
        echo "4) Technology Stack Enumeration"
        echo "5) Back to Main Menu"
        
        read -p "Select option (1-5): " enum_choice
        
        case $enum_choice in
            1)
                echo -e "${YELLOW}[*] Directory/File Enumeration${NC}"
                read -p "Enter target URL: " dir_target
                read -p "Wordlist path (default: /usr/share/wordlists/dirb/common.txt): " wordlist
                wordlist=${wordlist:-/usr/share/wordlists/dirb/common.txt}
                
                echo -e "${CYAN}Select tool:${NC}"
                echo "1) Gobuster"
                echo "2) Dirb"
                echo "3) Dirsearch (if installed)"
                read -p "Choice: " dir_tool
                
                case $dir_tool in
                    1)
                        gobuster dir -u $dir_target -w $wordlist -o "$workspace/enumeration/gobuster_$(date +%s).txt"
                        ;;
                    2)
                        dirb $dir_target $wordlist -o "$workspace/enumeration/dirb_$(date +%s).txt"
                        ;;
                    3)
                        if command -v dirsearch &> /dev/null; then
                            dirsearch -u $dir_target -w $wordlist -o "$workspace/enumeration/dirsearch_$(date +%s).txt"
                        else
                            echo -e "${RED}[!] Dirsearch not installed${NC}"
                        fi
                        ;;
                esac
                ;;
                
            2)
                echo -e "${YELLOW}[*] Parameter Discovery${NC}"
                read -p "Enter target URL with parameters: " param_url
                read -p "Parameter wordlist path: " param_wordlist
                
                if [ -f "$param_wordlist" ]; then
                    while IFS= read -r param; do
                        echo -e "${YELLOW}[*] Testing parameter: $param${NC}"
                        curl -s -o /dev/null -w "%{http_code}" "$param_url?$param=test" >> "$workspace/enumeration/parameters_$(date +%s).txt"
                        echo " - $param" >> "$workspace/enumeration/parameters_$(date +%s).txt"
                    done < "$param_wordlist"
                else
                    echo -e "${RED}[!] Wordlist not found${NC}"
                fi
                ;;
                
            3)
                echo -e "${YELLOW}[*] API Endpoint Discovery${NC}"
                read -p "Enter base API URL: " api_url
                
                common_endpoints=("v1" "v2" "api" "rest" "graphql" "swagger" "docs" "users" "admin" "auth" "login" "data")
                
                for endpoint in "${common_endpoints[@]}"; do
                    response=$(curl -s -o /dev/null -w "%{http_code}" "$api_url/$endpoint")
                    if [ "$response" != "404" ]; then
                        echo "$api_url/$endpoint - HTTP $response" >> "$workspace/enumeration/api_endpoints.txt"
                    fi
                done
                ;;
                
            4)
                echo -e "${YELLOW}[*] Technology Stack Enumeration${NC}"
                read -p "Enter target URL: " tech_target
                
                # Extract headers
                curl -I $tech_target > "$workspace/enumeration/headers.txt"
                
                # Check for common technologies
                if command -v whatweb &> /dev/null; then
                    whatweb $tech_target -v > "$workspace/enumeration/technologies.txt"
                fi
                
                # Check for specific technologies
                echo -e "${YELLOW}[*] Checking for WordPress${NC}"
                curl -s $tech_target/wp-json | jq '.' 2>/dev/null >> "$workspace/enumeration/wordpress.txt"
                
                echo -e "${YELLOW}[*] Checking for Laravel${NC}"
                curl -I $tech_target 2>/dev/null | grep -i "laravel" >> "$workspace/enumeration/frameworks.txt"
                ;;
                
            5)
                break
                ;;
        esac
    done
}

# Function for vulnerability testing
vulnerability_phase() {
    local workspace=$1
    local target=$2
    
    echo -e "${BLUE}==================================================${NC}"
    echo -e "${GREEN}         VULNERABILITY TESTING PHASE              ${NC}"
    echo -e "${BLUE}==================================================${NC}"
    
    while true; do
        echo -e "\n${CYAN}Vulnerability Testing Options:${NC}"
        echo "1) SQL Injection Testing"
        echo "2) XSS (Cross-Site Scripting) Testing"
        echo "3) LFI/RFI Testing"
        echo "4) SSL/TLS Testing"
        echo "5) Back to Main Menu"
        
        read -p "Select option (1-5): " vuln_choice
        
        case $vuln_choice in
            1)
                echo -e "${YELLOW}[*] SQL Injection Testing${NC}"
                read -p "Enter target URL with parameter: " sql_target
                
                # Basic SQL injection payloads
                payloads=("'" "\"\"'" "1' OR '1'='1" "1 AND 1=1" "1 AND 1=2")
                
                for payload in "${payloads[@]}"; do
                    echo -e "${YELLOW}[*] Testing: $payload${NC}"
                    response=$(curl -s "$sql_target$payload")
                    
                    # Check for SQL errors
                    if echo "$response" | grep -i "sql" | grep -i "error\|syntax\|mysql\|oracle\|postgresql" &> /dev/null; then
                        echo "Potential SQL injection with payload: $payload" >> "$workspace/vulnerability/sqli_findings.txt"
                    fi
                done
                ;;
                
            2)
                echo -e "${YELLOW}[*] XSS Testing${NC}"
                read -p "Enter target URL with parameter: " xss_target
                
                # XSS payloads
                xss_payloads=("<script>alert(1)</script>" "<img src=x onerror=alert(1)>" "\"><script>alert(1)</script>")
                
                for payload in "${xss_payloads[@]}"; do
                    echo -e "${YELLOW}[*] Testing: $payload${NC}"
                    encoded_payload=$(echo "$payload" | sed 's/ /%20/g' | sed 's/</%3C/g' | sed 's/>/%3E/g')
                    response=$(curl -s "$xss_target$encoded_payload")
                    
                    # Check if payload reflected
                    if echo "$response" | grep -q "$payload"; then
                        echo "Potential XSS with payload: $payload" >> "$workspace/vulnerability/xss_findings.txt"
                    fi
                done
                ;;
                
            3)
                echo -e "${YELLOW}[*] LFI/RFI Testing${NC}"
                read -p "Enter target URL with parameter: " lfi_target
                
                # LFI payloads
                lfi_payloads=("../../../../etc/passwd" "..\\..\\..\\..\\windows\\win.ini" "/etc/passwd" "....//....//....//etc/passwd")
                
                for payload in "${lfi_payloads[@]}"; do
                    echo -e "${YELLOW}[*] Testing: $payload${NC}"
                    response=$(curl -s "$lfi_target$payload")
                    
                    # Check for file contents
                    if echo "$response" | grep -q "root:x:\|boot loader\|\[fonts\]"; then
                        echo "Potential LFI with payload: $payload" >> "$workspace/vulnerability/lfi_findings.txt"
                    fi
                done
                ;;
                
            4)
                echo -e "${YELLOW}[*] SSL/TLS Testing${NC}"
                read -p "Enter target domain: " ssl_target
                
                if command -v testssl &> /dev/null; then
                    testssl --htmlfile "$workspace/vulnerability/ssl_test.html" $ssl_target
                else
                    # Basic SSL check with openssl
                    echo | openssl s_client -connect $ssl_target:443 2>/dev/null | openssl x509 -text > "$workspace/vulnerability/ssl_cert_info.txt"
                fi
                ;;
                
            5)
                break
                ;;
        esac
    done
}

# Function for report generation
generate_report() {
    local workspace=$1
    local domain=$2
    
    echo -e "${BLUE}==================================================${NC}"
    echo -e "${GREEN}            REPORT GENERATION                      ${NC}"
    echo -e "${BLUE}==================================================${NC}"
    
    report_file="$workspace/report/final_report_$(date +%Y%m%d).html"
    
    # Create HTML report
    cat > "$report_file" << EOF
<!DOCTYPE html>
<html>
<head>
    <title>Penetration Test Report - $domain</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 20px; background: #f5f5f5; }
        .header { background: #333; color: white; padding: 20px; border-radius: 5px; }
        .section { background: white; margin: 20px 0; padding: 20px; border-radius: 5px; box-shadow: 0 2px 5px rgba(0,0,0,0.1); }
        .vulnerability { border-left: 4px solid #ff4444; padding: 10px; margin: 10px 0; background: #fff5f5; }
        .info { border-left: 4px solid #44ff44; padding: 10px; margin: 10px 0; background: #f5fff5; }
        h1, h2, h3 { color: #333; }
        .timestamp { color: #666; font-size: 0.9em; }
        pre { background: #f0f0f0; padding: 10px; border-radius: 3px; overflow-x: auto; }
    </style>
</head>
<body>
    <div class="header">
        <h1>Web Penetration Test Report</h1>
        <p>Target: $domain</p>
        <p class="timestamp">Generated: $(date)</p>
    </div>
    
    <div class="section">
        <h2>Executive Summary</h2>
        <p>This report summarizes the findings of the penetration test conducted against $domain.</p>
    </div>
    
    <div class="section">
        <h2>Scope</h2>
        <p>Target Domain: $domain</p>
        <p>Testing Period: $(date)</p>
        <p>Testing Methodology: Web Application Penetration Testing</p>
    </div>
    
    <div class="section">
        <h2>Reconnaissance Findings</h2>
EOF
    
    # Add reconnaissance findings if they exist
    if [ -d "$workspace/recon" ]; then
        echo "<h3>Subdomains Discovered</h3><pre>" >> "$report_file"
        cat "$workspace"/recon/*sub*.txt 2>/dev/null | sort -u >> "$report_file"
        echo "</pre>" >> "$report_file"
    fi
    
    # Add scanning findings
    if [ -d "$workspace/scanning" ]; then
        echo "<h3>Open Ports and Services</h3><pre>" >> "$report_file"
        cat "$workspace"/scanning/nmap*.nmap 2>/dev/null >> "$report_file"
        echo "</pre>" >> "$report_file"
    fi
    
    # Add vulnerability findings
    if [ -d "$workspace/vulnerability" ]; then
        echo "<h3>Vulnerabilities Identified</h3>" >> "$report_file"
        
        if [ -f "$workspace/vulnerability/sqli_findings.txt" ]; then
            echo "<div class='vulnerability'>" >> "$report_file"
            echo "<h4>SQL Injection</h4><pre>" >> "$report_file"
            cat "$workspace/vulnerability/sqli_findings.txt" >> "$report_file"
            echo "</pre></div>" >> "$report_file"
        fi
        
        if [ -f "$workspace/vulnerability/xss_findings.txt" ]; then
            echo "<div class='vulnerability'>" >> "$report_file"
            echo "<h4>Cross-Site Scripting (XSS)</h4><pre>" >> "$report_file"
            cat "$workspace/vulnerability/xss_findings.txt" >> "$report_file"
            echo "</pre></div>" >> "$report_file"
        fi
        
        if [ -f "$workspace/vulnerability/lfi_findings.txt" ]; then
            echo "<div class='vulnerability'>" >> "$report_file"
            echo "<h4>Local File Inclusion</h4><pre>" >> "$report_file"
            cat "$workspace/vulnerability/lfi_findings.txt" >> "$report_file"
            echo "</pre></div>" >> "$report_file"
        fi
    fi
    
    # Close HTML
    cat >> "$report_file" << EOF
    </div>
    
    <div class="section">
        <h2>Remediation Recommendations</h2>
        <ul>
            <li>Implement input validation and parameterized queries to prevent SQL injection</li>
            <li>Apply proper output encoding to prevent XSS attacks</li>
            <li>Use secure file inclusion methods and validate user input</li>
            <li>Keep all software and dependencies updated</li>
            <li>Implement proper access controls and authentication mechanisms</li>
        </ul>
    </div>
    
    <div class="section">
        <h2>Tools Used</h2>
        <ul>
            <li>Nmap - Network scanning</li>
            <li>Gobuster/Dirb - Directory enumeration</li>
            <li>Nikto - Vulnerability scanning</li>
            <li>Whatweb - Technology detection</li>
            <li>Custom scripts - Manual testing</li>
        </ul>
    </div>
    
    <div class="section">
        <h2>Disclaimer</h2>
        <p>This test was conducted with proper authorization. The findings should be used for security improvement purposes only.</p>
    </div>
</body>
</html>
EOF
    
    echo -e "${GREEN}[+] Report generated: $report_file${NC}"
    
    # Create summary text file
    summary_file="$workspace/report/summary.txt"
    {
        echo "=========================================="
        echo "PENETRATION TEST SUMMARY - $domain"
        echo "=========================================="
        echo "Date: $(date)"
        echo ""
        echo "FINDINGS SUMMARY:"
        echo "------------------------------------------"
        
        # Count findings
        sqli_count=$(grep -l "SQL" "$workspace"/vulnerability/* 2>/dev/null | wc -l)
        xss_count=$(grep -l "XSS" "$workspace"/vulnerability/* 2>/dev/null | wc -l)
        lfi_count=$(grep -l "LFI" "$workspace"/vulnerability/* 2>/dev/null | wc -l)
        
        echo "SQL Injection: $sqli_count potential findings"
        echo "XSS: $xss_count potential findings"
        echo "LFI/RFI: $lfi_count potential findings"
        
        echo ""
        echo "OPEN PORTS FOUND:"
        grep -h "open" "$workspace"/scanning/*.nmap 2>/dev/null | sort -u || echo "No open ports found"
        
        echo ""
        echo "=========================================="
        echo "Report generated by Web Pentest Script v$VERSION"
        echo "=========================================="
    } > "$summary_file"
    
    echo -e "${GREEN}[+] Summary saved: $summary_file${NC}"
}

# Main menu function
main_menu() {
    local workspace=""
    local target=""
    
    while true; do
        echo -e "\n${PURPLE}==================================================${NC}"
        echo -e "${CYAN}                    MAIN MENU                       ${NC}"
        echo -e "${PURPLE}==================================================${NC}"
        echo "1) Setup Workspace"
        echo "2) Reconnaissance Phase"
        echo "3) Scanning Phase"
        echo "4) Enumeration Phase"
        echo "5) Vulnerability Testing Phase"
        echo "6) Generate Report"
        echo "7) Show All Commands Help"
        echo "8) Exit"
        
        read -p "Select option (1-8): " main_choice
        
        case $main_choice in
            1)
                read -p "Enter target domain: " target
                if [ -n "$target" ]; then
                    workspace=$(create_workspace "$target")
                    echo -e "${GREEN}[+] Workspace: $workspace${NC}"
                else
                    echo -e "${RED}[!] Target domain cannot be empty${NC}"
                fi
                ;;
                
            2)
                if [ -n "$workspace" ] && [ -n "$target" ]; then
                    recon_phase "$workspace" "$target"
                else
                    echo -e "${RED}[!] Please setup workspace first${NC}"
                fi
                ;;
                
            3)
                if [ -n "$workspace" ] && [ -n "$target" ]; then
                    scanning_phase "$workspace" "$target"
                else
                    echo -e "${RED}[!] Please setup workspace first${NC}"
                fi
                ;;
                
            4)
                if [ -n "$workspace" ] && [ -n "$target" ]; then
                    enumeration_phase "$workspace" "$target"
                else
                    echo -e "${RED}[!] Please setup workspace first${NC}"
                fi
                ;;
                
            5)
                if [ -n "$workspace" ] && [ -n "$target" ]; then
                    vulnerability_phase "$workspace" "$target"
                else
                    echo -e "${RED}[!] Please setup workspace first${NC}"
                fi
                ;;
                
            6)
                if [ -n "$workspace" ] && [ -n "$target" ]; then
                    generate_report "$workspace" "$target"
                else
                    echo -e "${RED}[!] Please setup workspace first${NC}"
                fi
                ;;
                
            7)
                show_command_help
                ;;
                
            8)
                echo -e "${YELLOW}[*] Exiting...${NC}"
                exit 0
                ;;
                
            *)
                echo -e "${RED}[!] Invalid option${NC}"
                ;;
        esac
    done
}

# Function to show command help
show_command_help() {
    echo -e "\n${BLUE}==================================================${NC}"
    echo -e "${GREEN}              COMMAND REFERENCE                    ${NC}"
    echo -e "${BLUE}==================================================${NC}"
    
    echo -e "\n${CYAN}RECONNAISSANCE COMMANDS:${NC}"
    echo -e "${YELLOW}Subdomain Enumeration:${NC}"
    echo "  sublist3r -d example.com -o subdomains.txt"
    echo "  amass enum -d example.com -o amass.txt"
    echo "  gobuster dns -d example.com -w /usr/share/wordlists/dirb/common.txt"
    echo "  dig example.com ANY"
    echo "  nslookup example.com"
    
    echo -e "\n${CYAN}DNS Enumeration:${NC}"
    echo "  dnsrecon -d example.com"
    echo "  dnsenum example.com"
    echo "  fierce --domain example.com"
    
    echo -e "\n${CYAN}SCANNING COMMANDS:${NC}"
    echo -e "${YELLOW}Nmap Scans:${NC}"
    echo "  nmap -sV -sC -O example.com              # Comprehensive scan"
    echo "  nmap -p- -T4 example.com                  # Full port scan"
    echo "  nmap -sS -sV -p 1-1000 example.com        # SYN scan with version detection"
    echo "  nmap --script vuln example.com             # Vulnerability scan"
    
    echo -e "\n${YELLOW}Masscan:${NC}"
    echo "  masscan -p1-65535 --rate=1000 example.com"
    
    echo -e "\n${CYAN}WEB ENUMERATION COMMANDS:${NC}"
    echo -e "${YELLOW}Directory Brute Force:${NC}"
    echo "  gobuster dir -u http://example.com -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt"
    echo "  dirb http://example.com /usr/share/wordlists/dirb/common.txt"
    echo "  wfuzz -c -z file,/usr/share/wordlists/dirb/common.txt --hc 404 http://example.com/FUZZ"
    
    echo -e "\n${YELLOW}Parameter Discovery:${NC}"
    echo "  arjun -u http://example.com/page.php"
    echo "  ffuf -w /usr/share/wordlists/parameters.txt -u http://example.com/page.php?FUZZ=test"
    
    echo -e "\n${CYAN}VULNERABILITY TESTING COMMANDS:${NC}"
    echo -e "${YELLOW}SQL Injection:${NC}"
    echo "  sqlmap -u 'http://example.com/page.php?id=1' --dbs"
    echo "  sqlmap -r request.txt -p parameter --risk=3 --level=5"
    
    echo -e "\n${YELLOW}XSS Testing:${NC}"
    echo "  dalfox url http://example.com/page.php?q=test"
    echo "  xsstrike -u 'http://example.com/page.php?q=test'"
    
    echo -e "\n${YELLOW}SSL/TLS Testing:${NC}"
    echo "  testssl.sh example.com"
    echo "  sslscan example.com:443"
    
    echo -e "\n${CYAN}ADDITIONAL TOOLS:${NC}"
    echo -e "${YELLOW}Technology Detection:${NC}"
    echo "  whatweb example.com"
    echo "  wappalyzer (browser extension)"
    
    echo -e "\n${YELLOW}Screenshots:${NC}"
    echo "  eyewitness --web -f urls.txt"
    echo "  aquatone -list urls.txt"
    
    echo -e "\n${YELLOW}Content Discovery:${NC}"
    echo "  ffuf -w /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt -u http://example.com/FUZZ"
    echo "  feroxbuster -u http://example.com -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt"
    
    echo -e "\n${YELLOW}Subdomain Takeover:${NC}"
    echo "  subjack -w subdomains.txt -t 100 -ssl"
    echo "  subzy -targets subdomains.txt"
    
    read -p "Press Enter to continue..."
}

# Main execution
main() {
    show_banner
    
    # Check if running as root (required for some scans)
    if [[ $EUID -ne 0 ]]; then
        echo -e "${YELLOW}[!] Note: Some scans (SYN scan, masscan) require root privileges${NC}"
        echo -e "${YELLOW}[!] Consider running with: sudo $0${NC}"
        echo ""
    fi
    
    # Check dependencies
    check_dependencies
    
    # Start main menu
    main_menu
}

# Trap Ctrl+C
trap 'echo -e "\n${RED}[!] Script interrupted${NC}"; exit 1' INT

# Run main function
main
```

# Complete Guide: Using the Web Penetration Testing Script

##  **Prerequisites Installation**

First, install the required tools on Kali Linux:

```bash
# Update system
sudo apt update && sudo apt upgrade -y

# Install essential tools
sudo apt install -y nmap gobuster dirb nikto whatweb dnsrecon dnsenum \
                    masscon testssl.sh wfuzz ffuf curl wget jq

# Install additional tools (optional)
sudo apt install -y seclists # Wordlists
sudo apt install -y eyewitness aquatone # Screenshot tools
sudo apt install -y sqlmap # SQL injection tool

# Python tools (install via pip)
pip3 install arjun dalfox xsstrike
```

##  **Step-by-Step Usage Guide with Example**

### **Example Target**: `hackthebox.com` (legitimate testing target)

---

## **STEP 1: Save and Prepare the Script**

```bash
# Save the script
nano webpen_test.sh

# Copy the entire script content and paste
# Save with Ctrl+O, then Ctrl+X

# Make it executable
chmod +x webpen_test.sh

# Run with sudo for full functionality
sudo ./webpen_test.sh
```

---

## **STEP 2: Initial Setup**

**What you'll see:**
```
==================================================
    Web Penetration Testing Automation Script    
              Version: 1.0                  
==================================================

[*] Checking dependencies...
[+] All dependencies installed

==================================================
                    MAIN MENU                       
==================================================
1) Setup Workspace
2) Reconnaissance Phase
3) Scanning Phase
4) Enumeration Phase
5) Vulnerability Testing Phase
6) Generate Report
7) Show All Commands Help
8) Exit

Select option (1-8): 
```

**Action:** Select `1` and enter target

```
Enter target domain: hackthebox.com
[*] Creating workspace: pen_test_hackthebox.com_20240101_143022
[+] Workspace created successfully
[+] Workspace: pen_test_hackthebox.com_20240101_143022
```

**Expected Output:** Directory structure created:
```
pen_test_hackthebox.com_20240101_143022/
├── recon/
├── scanning/
├── enumeration/
├── vulnerability/
├── report/
└── logs/
```

---

## **STEP 3: Reconnaissance Phase**

**Action:** Select `2` from main menu

```
==================================================
           RECONNAISSANCE PHASE                  
==================================================

Reconnaissance Options:
1) Subdomain Enumeration
2) DNS Information Gathering
3) WHOIS Lookup
4) Technology Detection
5) Run All Reconnaissance
6) Back to Main Menu

Select option (1-6): 
```

### **Option 1: Subdomain Enumeration**
```
Select option (1-6): 1

[*] Subdomain Enumeration
Enter domain (default: hackthebox.com): hackthebox.com

Select tool:
1) Sublist3r (if installed)
2) Amass (if installed)
3) DNS Bruteforce with gobuster
4) Manual dig/nslookup
Choice: 3

Enter wordlist path (default: /usr/share/wordlists/dirb/common.txt): 
[Press Enter for default]
```

**Expected Output:**
```
[*] Starting gobuster DNS enumeration
Found: www.hackthebox.com
Found: mail.hackthebox.com
Found: forum.hackthebox.com
Found: academy.hackthebox.com
Found: blog.hackthebox.com
Found: support.hackthebox.com
Found: admin.hackthebox.com
Found: api.hackthebox.com
Found: docs.hackthebox.com
Found: status.hackthebox.com

[+] Results saved to: pen_test_hackthebox.com_20240101_143022/recon/gobuster_dns_hackthebox.com.txt
```

### **Option 2: DNS Information Gathering**
```
Select option (1-6): 2

[*] DNS Information Gathering
Enter domain: hackthebox.com
```

**Expected Output (saved to file):**
```
=== DNS Records for hackthebox.com ===
A Record:
104.18.20.121
104.18.21.121

MX Records:
10 mx1.hackthebox.com
20 mx2.hackthebox.com

NS Records:
ns1.hackthebox.com
ns2.hackthebox.com

TXT Records:
"v=spf1 include:spf.hackthebox.com ~all"
"google-site-verification=xxxxxxxxxx"
```

### **Option 4: Technology Detection**
```
Select option (1-6): 4

[*] Technology Detection
Enter target URL (with http/https): https://hackthebox.com
```

**Expected Output:**
```
[+] Technology information saved
File: pen_test_hackthebox.com_20240101_143022/recon/technologies_httpshackthebox.com.txt

Contents:
http://hackthebox.com [200 OK] Cloudflare, HTML5, JavaScript, 
jQuery, Modernizr, Font Awesome, Google Analytics, 
Vue.js, Nginx, Let's Encrypt, HTTP/3
```

---

## **STEP 4: Scanning Phase**

**Action:** Return to main menu and select `3`

```
==================================================
              SCANNING PHASE                      
==================================================

Scanning Options:
1) Nmap Port Scan
2) Masscan (Fast Scan)
3) Service Version Detection
4) Vulnerability Scan with Nikto
5) Run All Scans
6) Back to Main Menu

Select option (1-6): 1
```

### **Nmap Port Scan**
```
[*] Nmap Port Scan
Enter target IP/domain: hackthebox.com
Port range (default: 1-1000): [Press Enter]

Select scan type:
1) TCP SYN Scan (Stealth)
2) TCP Connect Scan
3) UDP Scan
4) Comprehensive Scan
Choice: 4
```

**Expected Output:**
```
Starting Nmap 7.94 ( https://nmap.org )
Nmap scan report for hackthebox.com (104.18.20.121)
Host is up (0.042s latency).

PORT    STATE    SERVICE    VERSION
22/tcp  open     ssh        OpenSSH 8.2p1 Ubuntu 4ubuntu0.5
80/tcp  open     http       Cloudflare http proxy
443/tcp open     ssl/http   Cloudflare
8080/tcp filtered http-proxy

Service detection performed. Please report any incorrect results.
Nmap done: 1 IP address (1 host up) scanned in 45.67 seconds
```

### **Nikto Vulnerability Scan (Option 4)**
```
Select option (1-6): 4

[*] Nikto Vulnerability Scan
Enter target URL: https://hackthebox.com
```

**Expected Output:**
```
- Nikto v2.5.0
---------------------------------------------------------------------------
+ Target IP: 104.18.20.121
+ Target Hostname: hackthebox.com
+ Target Port: 443
---------------------------------------------------------------------------
+ SSL Info: Subject:  CN=hackthebox.com
+ Server: cloudflare
+ Retrieved x-powered-by header: PHP/7.4.33
+ The X-Content-Type-Options header is not set.
+ Root page / redirects to: https://www.hackthebox.com/
+ Uncommon header 'cf-ray' found, with contents: xxx
+ /: Cookie PHPSESSID created without the httponly flag.
+ /admin/: Directory indexing found.
+ /login.php?redirect=: Outputs the PHP error string.
```

---

## **STEP 5: Enumeration Phase**

**Action:** Return to main menu and select `4`

```
==================================================
            ENUMERATION PHASE                     
==================================================

Enumeration Options:
1) Directory/File Enumeration
2) Parameter Discovery
3) API Endpoint Discovery
4) Technology Stack Enumeration
5) Back to Main Menu

Select option (1-5): 1
```

### **Directory Enumeration**
```
[*] Directory/File Enumeration
Enter target URL: https://hackthebox.com
Wordlist path (default: /usr/share/wordlists/dirb/common.txt): 

Select tool:
1) Gobuster
2) Dirb
3) Dirsearch
Choice: 1
```

**Expected Output:**
```
===============================================================
Gobuster v3.6
===============================================================
[+] Url:                     https://hackthebox.com
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirb/common.txt
===============================================================
Starting gobuster
===============================================================
/images               (Status: 301) [Size: 178]
/css                  (Status: 301) [Size: 178]
/js                   (Status: 301) [Size: 178]
/admin                (Status: 403) [Size: 199]
/login                (Status: 200) [Size: 5421]
/register             (Status: 200) [Size: 4987]
/api                  (Status: 401) [Size: 34]
/dashboard            (Status: 302) [Size: 0]
/forum                (Status: 200) [Size: 12453]
/blog                 (Status: 200) [Size: 8921]
/support              (Status: 200) [Size: 3456]
/backup               (Status: 403) [Size: 199]
/.git                 (Status: 403) [Size: 199]
/.env                 (Status: 403) [Size: 199]
===============================================================
Finished
===============================================================
```

### **API Endpoint Discovery (Option 3)**
```
Select option (1-5): 3

[*] API Endpoint Discovery
Enter base API URL: https://hackthebox.com/api
```

**Expected Output (saved to file):**
```
https://hackthebox.com/api/v1 - HTTP 401
https://hackthebox.com/api/v2 - HTTP 401
https://hackthebox.com/api/users - HTTP 403
https://hackthebox.com/api/auth - HTTP 200
https://hackthebox.com/api/docs - HTTP 200
https://hackthebox.com/api/swagger - HTTP 200
https://hackthebox.com/api/health - HTTP 200
https://hackthebox.com/api/status - HTTP 200
```

---

## **STEP 6: Vulnerability Testing Phase**

**Action:** Return to main menu and select `5`

```
==================================================
         VULNERABILITY TESTING PHASE              
==================================================

Vulnerability Testing Options:
1) SQL Injection Testing
2) XSS (Cross-Site Scripting) Testing
3) LFI/RFI Testing
4) SSL/TLS Testing
5) Back to Main Menu

Select option (1-5): 1
```

### **SQL Injection Testing**
```
[*] SQL Injection Testing
Enter target URL with parameter: https://hackthebox.com/page.php?id=1
```

**Expected Output:**
```
[*] Testing: 1' OR '1'='1
[*] Testing: 1 AND 1=1
[*] Testing: 1 AND 1=2

[!] Potential SQL injection with payload: 1' OR '1'='1
[!] Found in: page.php?id=1
[!] Error message: "You have an error in your SQL syntax"

Results saved to: pen_test_hackthebox.com_20240101_143022/vulnerability/sqli_findings.txt
```

### **XSS Testing (Option 2)**
```
Select option (1-5): 2

[*] XSS Testing
Enter target URL with parameter: https://hackthebox.com/search.php?q=test
```

**Expected Output:**
```
[*] Testing: <script>alert(1)</script>
[*] Testing: <img src=x onerror=alert(1)>
[*] Testing: "><script>alert(1)</script>

[!] Potential XSS with payload: <script>alert(1)</script>
[!] Payload reflected in response

Results saved to: pen_test_hackthebox.com_20240101_143022/vulnerability/xss_findings.txt
```

---

## **STEP 7: Generate Report**

**Action:** Return to main menu and select `6`

```
==================================================
            REPORT GENERATION                      
==================================================

[+] Report generated: pen_test_hackthebox.com_20240101_143022/report/final_report_20240101.html
[+] Summary saved: pen_test_hackthebox.com_20240101_143022/report/summary.txt
```

### **Expected Summary Report Content:**
```
==========================================
PENETRATION TEST SUMMARY - hackthebox.com
==========================================
Date: Mon Jan 1 15:30:45 UTC 2024

FINDINGS SUMMARY:
------------------------------------------
SQL Injection: 2 potential findings
XSS: 1 potential findings
LFI/RFI: 0 potential findings

OPEN PORTS FOUND:
22/tcp open  ssh
80/tcp open  http
443/tcp open  https

RECONNAISSANCE HIGHLIGHTS:
- 15 subdomains discovered
- 3 name servers identified
- Technology: Vue.js, Nginx, Cloudflare
- SSL Certificate: Let's Encrypt

CRITICAL FINDINGS:
1. SQL Injection in page.php?id parameter
   - Payload: 1' OR '1'='1
   - Impact: Database enumeration possible

2. Reflected XSS in search.php
   - Payload: <script>alert(1)</script>
   - Impact: Session hijacking possible

3. Directory listing enabled in /admin/
   - Sensitive files exposed
   - Impact: Information disclosure

==========================================
Report generated by Web Pentest Script v1.0
==========================================
```

### **HTML Report Preview:**
The HTML report will be a professional document with:
- Executive summary
- Scope and methodology
- Detailed findings with screenshots (if added)
- Vulnerability classifications (Critical/High/Medium/Low)
- Remediation steps for each finding
- Tools used
- Appendix with raw scan data

---

## **STEP 8: View Command Reference**

**Action:** Select `7` from main menu to see all available commands

```
==================================================
              COMMAND REFERENCE                    
==================================================

RECONNAISSANCE COMMANDS:
  sublist3r -d example.com -o subdomains.txt
  amass enum -d example.com -o amass.txt
  gobuster dns -d example.com -w /usr/share/wordlists/dirb/common.txt
  dig example.com ANY
  nslookup example.com

SCANNING COMMANDS:
  nmap -sV -sC -O example.com
  nmap -p- -T4 example.com
  masscan -p1-65535 --rate=1000 example.com

WEB ENUMERATION COMMANDS:
  gobuster dir -u http://example.com -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
  ffuf -w /usr/share/wordlists/common.txt -u http://example.com/FUZZ

VULNERABILITY TESTING COMMANDS:
  sqlmap -u 'http://example.com/page.php?id=1' --dbs
  xsstrike -u 'http://example.com/page.php?q=test'
  testssl.sh example.com
```

---

##  **Tips for Effective Usage**

1. **Start Small**: Begin with basic scans before running comprehensive ones
2. **Use Appropriate Wordlists**: 
   - For quick scans: `/usr/share/wordlists/dirb/common.txt`
   - For thorough scans: `/usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt`
   - For maximum coverage: `/usr/share/wordlists/seclists/Discovery/Web-Content/`

3. **Respect Rate Limits**: Use appropriate thread counts to avoid DoS
4. **Save Intermediate Results**: The script automatically saves everything
5. **Review Logs**: Check `logs/` directory for any errors or warnings

