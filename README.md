# Verge-ASPNET-Review
API devloped using Microsoft Entity Framework 6

3 Models devloped:

## Asset Model
| Property Name     | Type           | Description                   | Default Value              |
| ----------------- | -------------- | ----------------------------- | -------------------------- |
| _Asset ID_        | int            | SQL Primary Key               | Not assigned/Autoincrement |
| _Type ID_         | AssetType      | Type of asset i.e. drone      | Required                   |
| _Table Key_       | int            | Key of asset in related table | Required                   |
| _Organization Id_ | OrganizationId | Id of owning organization     | -1/Unowned                 |

#### AssetType Enumeration
| Name        | int Id |
|-------------|--------|
| Drone       | 0      |
| Battery     | 1      |
| BaseStation | 2      |
| Gateway     | 4      |
| SmartCase   | 8      |

#### OrganizationId Enumeration

| Name     | int Id |
|----------|--------|
| Unowned  | -1     |
| Verge    | 0      |
| Strictly | 1      |
| Go       | 2      |

## Drone Model
| Property Name  | Type   | Description                 | Default Value/Params       |
|----------------|--------|-----------------------------|----------------------------|
| _Drone ID_     | int    | SQL primary key             | Not assigned/Autoincrement |
| _Drone UID_    | int    | Unique identifier for drone | Required/Unique            |
| _Faa ID_       | string | Unique FAA identifier       | null/Unique                |
| _Flight Hours_ | int    | Amount of flight time       | 0                          |
| _Firmware_     | string | Current firmware version    | ""                         |

## Battery Model
| Property Name    | Type | Description                        | Default Value/Params       |
|------------------|------|------------------------------------|----------------------------|
| _Battery ID_     | int  | SQL primary key                    | Not assigned/Autoincrement |
| _Battery Cycles_ | int  | Charge/Discharge cycles of battery | 0                          |
| _BatteryType_    | int  | External/Internal battery, 0/1     | Required                   |

## Developed URL requests:
| Resource                   | Type   | Description                      | 
| -------------------------- | ------ | -------------------------------- |
| `/v1/assets`               | `GET`  | Returns all assets               |
| `/v1/assets{id}`           | `GET`  | Gets an asset by id              |
| `/v1/assets/reassign/{id}` | `PUT`  | Reassigns ownership of an asset  |
| `/v1/assets/drone`         | `POST` | Creates new drone asset          |
| `/v1/assets/battery`       | `POST` | Creates new battery asset        |

## Data Input
Posting a new specific asset such as a drone requires **form data** containing all relevant model information. No primary key needs to be provided.
Each model is inherited by a _form model_, which implements organization information, to properly create a new asset entry.
Due to this, an organization id must also be provided in the form data to properly assign.

## Instructions
Update default connection string as needed in `appsettings.json` and `launchsettings.json` to proper localhost ports. Execution should default to running the swagger UI to test the defined models and controllers.
