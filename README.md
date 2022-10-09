
# WaterNSW WaterInsights for Home Assistant

![Dam level sensor dashboard example](https://github.com/battlemoose/waternsw-waterinsights-ha/blob/main/assets/dashboard-level-example.png)

This [Home Assistant](https://www.home-assistant.io/) component integrates NSW dam level and capacity data from the WaterNSW WaterInsights API as [sensors](https://www.home-assistant.io/integrations/sensor/) in the Home Assistant platform.

## Installation
 
The simplest method to install this integration is using [HACS](https://hacs.xyz/).

Manual installation can also be performed by:

 1. Creating a new directory named `waterinsights` in the `custom_components` directory of your Home Assistant configuration
 1. Copying the contents of this repository into the new `waterinsights` directory
 1. Restarting Home Assistant

## Usage

The `waterinsights` integration can currently only be configured via [Home Assistant's YAML configuration](https://www.home-assistant.io/docs/configuration/).

To add dam level sensors:

 1. Obtain an API key/secret
     1. Visit https://api.nsw.gov.au/Product/Index/26
     1. CLick the blue **Subscribe** button
     1. Log in or create an account
     1. Create an app that subscribes to the [WaterInsights from WaterNSW](https://api.nsw.gov.au/Product/Index/26) API
     1. Your API key and secret will be listed under the details page of your new app
 1. Find your dam ID(s)
     1. Visit https://waterinsights.waternsw.com.au/
     1. Search for a dam in the search box at the top of the page and click on a result in the dropdown that appears
     1. The number that appears to the left of the dam name in the search bar on the resulting page is the dam ID
     1. Repeat for any subsequent dams you also want to add sensors for
 1. Configure Home Assistant
     1. Create a new entry in your [Home Assistant `secrets.yaml` file](https://www.home-assistant.io/docs/configuration/secrets/) named `water_insights_api_secret` who's value is your API secret from step 1
     1. Add the following lines to your Home Assistant `configuration.yaml`. If the `sensor` key already exists, add the `- platform: waterinsights` element under the existing key.
        
        ``` yaml
        sensor:
          - platform: waterinsights
            api_key: /Insert your API key from step 1/
            api_secret: !secret water_insights_api_secret
            dams:
              - dam_id: /Insert a dam ID/
                name: /Insert an optional name/
              # For example
              - dam_id: "212243"
                name: "Warragamba Dam"
              - dam_id: "412106"
        ```

        The `name` key is optional for each dam. If not specified, the name returned by the API will be used.
     1. Restart Home Assistant. Your new dam sensors should show up as entities in your Home Assistant instance.