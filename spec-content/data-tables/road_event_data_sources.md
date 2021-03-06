# road_event_data_sources
**Required**

The `road_event_data_sources` table stores information about the data sources used to build the work zone data feed.
- Feeds must contain at least one data source, via an object in the `data_sources` array on the `road_event_feed_info`.
- `road_event` features are related to a `road_event_data_source` via the `road_event_data_source.data_source_id` member.

## Road Event Data Sources Table Structure
Field Name | Data Type | Description | Conformance | Notes
--- | --- | --- | --- | ---
**data_source_id** | ID | Unique identifier for the organization providing work zone data. | Required | Primary key. Linked to [road_events](/spec-content/data-tables/road_events.md) table via `road_events.data_source_id`.
**feed_info_id** | ID | Identifies the feed to which a data source is related. | Required | Foreign Key to `road_event_feed_info` for building a feed from the data tables.
**organization_name** | Text | The name of the organization for the authoritative source of the work zone data. | Required | Example: County DOT
**location_method** | Enumeration; Text | The typical method used to locate the beginning and end of a work zone impact area. | Required | See [Location Method Enumerated Type](/spec-content/enumerated-types/location_method.md)
**update_date** | DateTime | The UTC date and time when the data source was last updated. | Optional | All datetime formats shall follow [RFC 3339 Section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). Example: `2016-11-03T19:37:00Z`
**update_frequency** | Integer | The frequency in seconds at which the data source is updated. | Optional |
**contact_name** | Text | The name of the individual or group responsible for the work zone data source. | Optional | Example: Jo Help
**contact_email** | Text | The email address of the individual or group responsible for the data source. | Optional |
**location_verify_method** | Text | The method used to verify the accuracy of the location information. | Optional | Example: Survey accurate GPS equipment accurate to 0.1 cm
**lrs_type** | Text | Describes the type of linear referencing system (LRS) used for the milepost measurements. | Optional | Example: Use of milemarkers posted by the roadways. These are registered to a dynamic segmentation of statewide LRS basemap.
**lrs_url** | URL | A URL where additional information on the LRS information and transformation information is stored. | Optional | Example https://aaa.bbb.com/lrs
