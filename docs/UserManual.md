# Splunk EclecticIQ Endpoint Response User Manual

##   Introduction
###  EclecticIQ Endpoint Response

* EclecticIQ Endpoint Response is designed to improve cyber defenders' effectiveness and efficiency in threat hunting, monitoring, detection, and incident response.
* It gives service providers such as incident response (IR) companies and managed security service providers (MSSPs) the broadest investigation and response capabilities from a single agent available.
* Key features include a single lightweight and customizable os query-based agent for real-time detection & response; exceptionally broad telemetry coverage for optimized visibility; an easy-to-use alert management and investigation workflow; and full API access to telemetry and response.

### Prerequisites
* Splunk Enterprise version 8.2
* EclecticIQ will send the data to Splunk over TCP/UDP or Splunk HTTP Collector.

## Installation of Splunk Enterprise
 Refer to this manual to install the Splunk Enterprise.

[https://docs.splunk.com/index.php?title=Documentation:Splunk:Installation:Beforeyouinstall:8.1.0&action=pdfbook&version=8.2.2&product=Splunk].
### Installation for both APP & Addon
1. Open Splunk Enterprise
2. Click on Find More Apps
3. Enter the app name to search for EclecticIQ Endpoint Response
4. Check the prerequisites and details
5. Click on Install

### Installation for both APP & Addon(From File)

1. Login to Splunk Enterprise
2. Navigate to Manage Apps and click

   ![image](/docs/pics/1.png)

3. Click on "Install app from file"

   ![image](/docs/pics/2.png)
4. Install App From File pop-up window will appear
5. Click on Choose file
6. Choose the file and click on open 
7. Check the Upgrade checkbox
8. Click on the Upload button

   ![image](/docs/pics/3.png)
9. Successfully installed message will be displayed

   ![image](/docs/pics/4.png)
10. Go to Settings dropdown
11. Click on Server controls
12. Click on the Restart Splunk button
   ![image](/docs/pics/5.png)
13. Click on OK in the Pop-up window 
   ![image](/docs/pics/6.png)

After installation, We can see the Addon and App in Apps dropdown list

   ![image](/docs/pics/7.png) 


## Splunk Addon


### Working
The user needs to perform the following after Addon installation
#### EclecticIQ Endpoint Response data injection and parsing
1. Users need to create an index (optional) to store the EclecticIQ Endpoint Response events 
    
   **Steps for creating an Index**

    1. Login to Splunk Enterprise
    2. Go to the Settings dropdown
    3. Click on indexes
    4. Click on New Index
    5. Enter the Index name[Eg: index = “er_data”] and fill all the fields and click on save.
    ![image](/docs/pics/8.png)
    
   **Steps for creating macros**

    1. Login to Splunk Enterprise
    2. Go to the Settings dropdown
    3. Click on Advanced search
    4. Click on Search macros
    5. Select New Search Macro
    6. Select EclecticIQ Endpoint Response Addon for Splunk in destination app dropdown.
    7. Enter the Name field[Eg: eiq_er_index]
    8. Replace `er_data` with the index name where Endpoint Response data is stored in the Definition field
    9. Click on Save button.
    ![image](/docs/pics/9.png)    
  

2. Create an HTTP Event Collector(HEC), TCP, or UDP on Splunk by selecting the index and source type name as “eclecticiq:er:json”
  
   **Note:** For parsing the fields from EclecticIQ Endpoint Response events the parsing logic is written under the source type named “eclecticiq:er:json”.
   
   **Steps for creating an HTTP Event Collector input**
   
    1. Login to Splunk Enterprise
    2. Go to the settings dropdown
    3. Click on Data inputs
    4. Click on HTTP Event Collector
    5. Click on New Token
    6. Fill all the fields and click on Next
    7. Select value `eclecticiq:er:json` from Source type dropdown 
    8. Select the Index name 
    9. Click on Review and Click on Submit
    ![image](/docs/pics/10.png)   
  
   **Steps for creating TCP input**
    
    1. Login to Splunk Enterprises
    2. Go to the Settings dropdown
    3. Click on Data inputs
    4. Click on TCP
    5. Click on New Local TCP
    6. Select TCP and enter the Port number and click on Next
    7. Select value `eclecticiq:er:json` from Source type dropdown  
    8. Select App context as `EclecticIQ Intelligence Centre Addon for Splunk` from the dropdown
    9. Select Host 
     * If select IP as Host. value of host field will set as IP Address of data sender.
   * If select DNS as Host. value of host field will set as Domain Name of data sender.
   * If select custom, value of host field will set as given value.
    10. Select the Index name
    11. Click on Review and Click on Submit
   ![image](/docs/pics/11.png)   
  
   **Steps for creating UDP input**
                                                                                                
   1. Login to Splunk Enterprises
   2. Go to the Settings dropdown
   3. Click on Data inputs
   4. Click on UDP
   5. Click on New Local UDP
   6. Select TCP and enter the Port number and click on Next
   7. Select value `eclecticiq:er:json` from Source type dropdown 
   8. Select App context as `EclecticIQ Intelligence Centre Addon for Splunk` from the dropdown
   9. Select Host
   * If select IP as Host. value of host field will set as IP Address of data sender.
   * If select DNS as Host. value of host field will set as Domain Name of data sender.
   * If select custom, value of host field will set as given value.
   10. Select the Index name
   11. Click on Review and Click on Submit
   ![image](/docs/pics/12.png)   

  
3. Use the created HTTP Event Collector token or TCP or UDP in the EclecticIQ platform to send events to Splunk



## Splunk App



### Dashboards
#### EclecticIQ Endpoint Response Dashboard
This dashboard shows the EclecticIQ Endpoint Response events ingested in Splunk. All the data searching queries are SPL queries to populate the data from the indexes.
1. Login to Splunk
2. Navigates to Apps > EclecticIQ Endpoint Response App for Splunk
(
* This dashboard is having the following filters:
  *   Time Range: This filter is used to view the particular events based on the time range by selecting the time from the Time Range dropdown filter( Default:24 hours)
  *   Search: User can filter the events based on keyword present in raw events.(Textbox Default: *).
  *   Radio button(which shows the events which has caused the alert)
         *  The options are True/False. 
* This dashboard is having the following panels :
  *  Endpoint Response Events table:  This is a table containing the events information ingested from the  Endpoint Response device.
  *  The table contains the following column fields,
     *  Time: Timestamp when the events occurred in ER
     *  Hostname: Host name of the event
     *  OS: Type of the OS these events are captured from
     *  Observable value: These fields are only available when the radio button is selected to "True". Whenever there is a match with observable, the matching Observable value is shown in this column.
     *  Observable maliciousness: The matching Observable maliciousness will be shown in this column.
     
* When clicking on the False Radio button this dashboard shows all the events ingested from the Endpoint Response

  ![image](/docs/pics/13.png)

* When clicking on the True button this dashboard shows the events which are matched with the data of EclecticIQ Intelligence Centre Addon Observables and which have caused some alerts(Via. Saved Search or Alert action) 

  ![image](/docs/pics/14.png)


#### ER Drilldown Dashboard
This dashboard screen will be displayed whenever a user clicks on any events row in the EclecticIQ Endpoint Response Dashboard.
* Filter:
     * Timerange: This filter is used to view the particular events based on the time range by selecting the time from the Timerange dropdown filter(Default: ±30 minutes)
      
* Panels :
  * Events related to Pid/Guid Table: This table displays all the events which are related to the clicked row in the EclecticIQ Endpoint Response dashboard
    * All the fields of the events will be shown here
    * If an alert is created(i.e, sighting) observable_id, value_eiq, and confidence_eiq values of observable will be displayed 
  * Timecharts: This chart will display the count of events as the floated points that are related to clicked events on the main dashboard
  * If the EclecticIQ Intelligence centre application is installed then two charts will be displayed or else only one chart will be displayed
    * Events with Pid/Guid for which the alert is not created: In this timechart, only those events which are not created any alert are displayed as floated points
    * Events with Pid/Guid for which the alert is created: If the sighting is created for triggered alert then only the events are displayed as floated points.

  ![image](/docs/pics/15.png)

  ![image](/docs/pics/16.png)

## Saved Searches
The app will provide the saved searches which will be used to map the data from EclecticIQ Endpoint Response with the threat intelligence data collected by the EclecticIQ Intelligence Center Splunk Addon in KV store lookups.

follow the below steps to match the data and create an alert 
* Go to Search, reports, and alerts
* From App dropdown select EclecticIQ Endpoint Response App for Splunk
* Go to Owner dropdown and click on All
* Click on EclecticIQ ER alert
* Click on Edit dropdown and select Edit Schedule
* Check on the "Schedule Report" checkbox in the Edit Schedule popup window
* Select the Schedule and Time Range 
* Click on Save
* Click on Edit > Enable

  ![image](/docs/pics/17.png)

To create the sightings follow below steps
* Go to Search, reports, and alerts
* From App dropdown select EclecticIQ Endpoint Response App for Splunk
* Go to Owner dropdown and click on All
* Click on EclecticIQ ER alert and copy the search query
* Click on cancel button 
* Click on New Alert
* Enter the unique name of the alert
* Paste the copied search in the search query but remove last line (outputlookup command)
* Adjust the schedule and trigger conditions
* Click on Add action 
* Select `Create Sighting` action from dropdown
* Enter the fields to send with the sighting
* Click on Save
* Click on Edit > Enable















