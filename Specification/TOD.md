# Time of Day files

Four time-of-day files handle day-of-week and time-of-day restrictions and other attributes on links, segments, lanes, lane_segments and movements

# time_set_definitions
The specification currently allows for times of day to be represented in the following format: 
`XXXXXXXX_HHMM_HHMM`, where `XXXXXXXX` is a bitmap of days of the week, Sunday-Saturday, Holiday. The HHMM are the start and end times. This is adapted from the Synchro Universal Traffic Data Format (UTDF) TimeOfDay table structure. For example, Monday-Friday 0700-0900 would be `01111100_0700_0900`. Alternatively, these can be coded in the following time_set_definitions table and `timeday_id` referenced instead of this format. 

Field Name | Type |  Description
-- | -- | --
timeday_id | ID | Primary key, similar to service_id in GTFS. Unique name of the time of day. Preferable legible rather than a number.
monday | boolean | whether Mondays are included (and so on for the other boolean fields)
tuesday | boolean | 0 or 1
wednesday | boolean | 0 or 1
thursday | boolean | 0 or 1
friday | boolean | 0 or 1
saturday | boolean | 0 or 1
sunday | boolean | 0 or 1
holiday | boolean | 0 or 1
start_time | timeofday | HH:MM  (24hr format)
end_time | timeofday | HH:MM  (24hr format)

Optional ad-hoc fields could define other types of day (`snow`, `unknown`, etc.).

# link_tod

link_tod is an optional file that handles day-of-week and time-of-day
restrictions on links. It is used for tolls (which may differ by
time-of-day), and part-time changes in link capacity. Since tolls often vary by time of day, they are placed in
this file.

link_tod data dictionary

| Field			| Type 			| Required? | Comment									|
| ------------- | ------------- | --------- | ----------------------------------------- |
| link_tod\_id  | Link_TOD\_ID  | Required  | Primary key                               |
| link\_id 		| Link\_ID 		| Required  | Foreign key, link table                    |
| time_day      | TimeDay\_Set 	| Conditionally required  | Define the availability/role of lane at different dates and times (either time_day or timeday_id is required   |
| timeday_id      | TimeDay\_ID 	| Conditionally required  | Used if times-of-day are defined on the time_set_definitions table   |
| capacity 		| INTEGER 		| Optional  | 											 |
| freespeed		| INTEGER		| Optional	|											|
| lanes			| INTEGER		| Optional	|											|
| bike\_facility	| TEXT			| Optional	|											|
| ped\_facility	| TEXT			| Optional	|											|
| parking	| TEXT			| Optional	|											|
| allowed\_uses | Use\_Set      | Required  |                                           |
| toll          | INTEGER       | Optional  | cents                                     |
| notes         | TEXT          | Optional  |                                           |

# segment_tod

segment_tod is an optional file that handles day-of-week and time-of-day restrictions on segments. 
It is used for part-time changes in segment capacity and number of lanes.

segment_tod data dictionary

| Field			| Type 			| Required? | Comment									|
| ------------- | ------------- | --------- | ----------------------------------------- |
| segment\_tod\_id  | Segment\_TOD\_ID  | Required  | Primary key                               |
| segment\_id 	| Segment\_ID 	| Required	| Foreign key, segment table.  |
| time_day      | TimeDay\_Set 	| Conditionally required  | Define the availability/role of lane at different dates and times (either time_day or timeday_id is required   |
| timeday_id      | TimeDay\_ID 	| Conditionally required  | Used if times-of-day are defined on the time_set_definitions table   |
| capacity 		| INTEGER 		| Optional  | 											 |
| freespeed		| INTEGER		| Optional	|											|
| lanes			| INTEGER		| Optional	|											|
| l\_lanes\_added	| INTEGER		| Optional	|											|
| r\_lanes\_added	| INTEGER		| Optional	|											|
| bike\_facility	| TEXT			| Optional	|											|
| ped\_facility	| TEXT			| Optional	|											|
| parking	| TEXT			| Optional	|											|
| allowed\_uses | Use\_Set      | Required  |                                           |
| toll          | INTEGER       | Optional  | cents                                     |
| notes         | TEXT          | Optional  |                                           |

# link_lane_tod

| Field			| Type 			| Required? | Comment									|
| ------------- | ------------- | --------- | ----------------------------------------- |
| link_tod\_id  | Link_TOD\_ID  | Required  | Primary key                               |
| link\_id 		| Link\_ID 		| Required  | Foreign key, link table                    |
| time_day      | TimeDay\_Set 	| Conditionally required  | Define the availability/role of lane at different dates and times (either time_day or timeday_id is required   |
| timeday_id      | TimeDay\_ID 	| Conditionally required  | Used if times-of-day are defined on the time_set_definitions table   |
| lane\_num      | INTEGER       | Required  |   |
| allowed\_uses  | Use\_Set     | Required  |   |
| r_barrier      | TEXT         | Optional  |    |
| l_barrier      | TEXT         | Optional   |    |
| width          | DOUBLE       | Optional   |    |
| notes          | TEXT         | Optional   |     |

# segment_lane_tod

| Field			| Type 			| Required? | Comment									|
| ------------- | ------------- | --------- | ----------------------------------------- |
| segment\_tod\_id  | Segment\_TOD\_ID  | Required  | Primary key                               |
| segment\_id 	| Segment\_ID 	| Required	| Foreign key, segment table.  |
| time_day      | TimeDay\_Set 	| Conditionally required  | Define the availability/role of lane at different dates and times (either time_day or timeday_id is required   |
| timeday_id      | TimeDay\_ID 	| Conditionally required  | Used if times-of-day are defined on the time_set_definitions table   |
| lane\_num      | INTEGER       | Required  |   |
| allowed\_uses  | Use\_Set     | Required  |   |
| r_barrier      | TEXT         | Optional  |    |
| l_barrier      | TEXT         | Optional   |    |
| width          | DOUBLE       | Optional   |    |
| notes          | TEXT         | Optional   |     |

Ad hoc fields may also be added to any of these tables.
