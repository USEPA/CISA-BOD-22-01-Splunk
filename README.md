# CISA-BOD-22-01-Splunk
This is a Splunk dashboard and report to monitor and report Knowen Exploited Vulnerabilities (KEV) that are detected by Tenable.  The code can be modified to use other vulnerability sources.

## Installation Instructions
### Create the Lookup Table
1.	Download CISA's Known Exploited Vulnerabilities list as a .csv file from https://www.cisa.gov/known-exploited-vulnerabilities-catalog
2. Upload it into Splunk as a lookup table.  We set ours to be readable by all apps and users.  You can name your lookup table known_exploited_vulnerabilities.csv
3. We use Splunk on prem and scheduled a cron job to download the csv file from CISA's site each evening.  Detailed instructions on this comin soon.  For now, you could use CISA's link to "Subscribe to the Known Exploited Vulnerabilities Catalog Update Bulletin" and manually update your lookup table.
### Create the Dashboard in Splunk
1. Create a new XML dashboard.  Ours was named "VMT - KEV Status"
2. Edit the source code of the dashboard you created
3. Copy the contents of "vmt - kev status.xml" in this repository
4. Paste the contents into your dashboard source code
5. You'll need to make the following changes to the attached XML dashboard:
   - Replace <<YOUR_INDEX>> with your index name on lines 5, 120, 140, 143
   - If you used a different lookup table name than known_exploited_vulnerabilities.csv, update it on lines 27 and 29.
   - If you want to remove the other choice from the dropdown, delete line 28, <choice value="vmt-kev-other.csv">other</choice>
   - Update the <label> attribute if you changed the name of your dashboard
6. Save your changes
### Schedule the Report (Optional)
This contains the search to build the export for the CyberScope BOD report.
1. Copy the contents of "bod-report.txt" in this repository
2. Create a new search and paste the search string from step 1 above
    - Replace <<YOUR_INDEX>> with your index name on line 4
    - If you used a different lookup table name, update it on lines 1, 5 and 10.
3. Make sure the search timeframe is not less than your Tenable scan frequency
4. We have ours set as a scheduled search to email the results as a csv file  
  
## Disclaimer
Disclaimer: The United States Environmental Protection Agency (EPA) GitHub project code is provided on an "as is" basis and the user assumes responsibility for its use. EPA has relinquished control of the information and no longer has responsibility to protect the integrity, confidentiality, or availability of the information. Any reference to specific commercial products, processes, or services by service mark, trademark, manufacturer, or otherwise, does not constitute or imply their endorsement, recommendation or favoring by EPA. The EPA seal and logo shall not be used in any manner to imply endorsement of any commercial product or activity by EPA or the United States Government.
