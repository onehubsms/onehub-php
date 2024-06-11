# Onehub PHP Sending SMS Library
```PHP
$x_username           = "";
$x_apikey             = "";

$params = array(
    "phoneNumbers"=> "+25472*******,+25473*******,+25474*******",
    "message"=>      "Hello api!",
    "senderId"=>     "Your-Sender-ID-Here",
);

$data = json_encode($params);

$sendMessageURL     = "https://api.onehub.co.ke/v1/sms/send";

$req                  = curl_init($sendMessageURL);

curl_setopt($req, CURLOPT_CUSTOMREQUEST, "POST");
curl_setopt($req, CURLOPT_TIMEOUT, 60);
curl_setopt($req, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($req, CURLOPT_RETURNTRANSFER, true);
curl_setopt($req, CURLOPT_POSTFIELDS, $data);
curl_setopt($req, CURLOPT_HTTPHEADER, array('Content-Type: application/json','x-api-user: '.$x_username,'x-api-key: '.$x_apikey));

$res              = curl_exec($req);

curl_close($req);

print_r($res);
```
# Username and API Key
You can get your username and API Key [here](https://dashboard.onehub.co.ke/account/0/user/signup).
# Request Body Parameters
`phoneNumbers` - `[Type: String]` `[Required]` - Phone numbers of the recipients in international format with the plus (+) sign. Multiple numbers should be comma-separated.

`Message` - `[Type: String]` `[Required]` - The message you want to send. Each message is counted as 160 characters long. Messages longer than 160 characters will be billed accordingly.

`Sender ID` - `[Type: String]` `[Required]` - A sender ID serves as a branding for outgoing messages, typically representing your company name. Your users will receive messages with your specified sender ID. You can apply for your sender ID on our [website](https://onehub.co.ke/).
# Response Body Parameters
## Response in case of successful sending of a message:
```json
{
    "0":{
        "country":"kenya",
        "cost":"KES 2.00",
        "success":[
            "+2547XXXYXXXX",
            "+2547XXXXXXXX"
        ]
    },
    "status":200,
    "message":"Message sent"
}
```
## Response in case a message fails:
```json
{
   "0":{
      "country":"kenya",
      "cost":"KES 1.00",
      "success":[
         "+2547XXXYXXXX"
      ],
      "failed":[
         "+2547XXXXXXXX"
      ]
   },
   "status":200,
   "message":"Message sent"
}
```
## Response in case of wrong credentials:
```json
{
    "status":401,
    "message":"Unauthorized"
}
```
# Onehub Add Contacts PHP library
```PHP
// authentication
$x_username      = "";
$x_apikey        = "";

// data
$createContact   = array(
    "name"       => "John Migo", # contact name
    "phone"      => "+254711xxxxxx", # international format
    "tags"       => "developer,nairobi", # optional comma separated tags
    "groups"     => "Nairobi Coding, Group 2" # optional groups to add contact
);

// endoint
$addContactURL     = "https://api.braceafrica.com/v1/contacts/add";

// encoding params
$params            = json_encode($createContact);
$req               = curl_init($addContactURL);

curl_setopt($req, CURLOPT_CUSTOMREQUEST, "POST");
curl_setopt($req, CURLOPT_TIMEOUT, 60);
curl_setopt($req, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($req, CURLOPT_RETURNTRANSFER, true);
curl_setopt($req, CURLOPT_POSTFIELDS, $params);
curl_setopt($req, CURLOPT_HTTPHEADER, array(
    'Content-Type: application/json',
    'Content-Length: '.strlen($params),
    'x-api-user: '.$x_username,
    'x-api-key: '.$x_apikey
));

// read api response
$res              = curl_exec($req);

// close curl
curl_close($req);

// print the raw json response
var_dump($res);
```
# Request Body Parameters
`name` - `[Type: String]` `[Required]` 

`phone` -	`[Type: String]` `[Required]` - Must be in international format.

`tags` - `[Type: String]`	`[Optional]` - A unique field to help group contacts e.g football,team,family.

`groups` - `[Type: String]`	`[Optional]` - This is a group name that the contacts will be added to. It must be an existing group.
# Response Body Parameters
## Response in case of successful adding of a contact:
```json
{
    "status": 200,
    "message": "Contact added"
}
```
# Onehub Edit Contacts PHP library
```PHP
// authentication
$x_username      = "";
$x_apikey        = "";

// data
$editContactData   = array(
    "name"       => "John New", # new contact name
    "phone"      => "+254711xxxxxx", # new phonenumber - international format
    "tags"       => "Edited Tag 1, Edited Tag", # new tags - comma separated tags
    "groups"     => "New Group1" # new groups - optional groups to link contact
);

// id of contact to edit: this can be gotten from the fetch contacts api
$contactId          = "1";

// endoint
$editContactURL     = "https://api.braceafrica.com/v1/contacts/edit/".$contactId;

// encoding params
$params             = json_encode($editContactData);
$req                = curl_init($editContactURL);

curl_setopt($req, CURLOPT_CUSTOMREQUEST, "POST");
curl_setopt($req, CURLOPT_TIMEOUT, 60);
curl_setopt($req, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($req, CURLOPT_RETURNTRANSFER, true);
curl_setopt($req, CURLOPT_POSTFIELDS, $params);
curl_setopt($req, CURLOPT_HTTPHEADER, array(
    'Content-Type: application/json',
    'Content-Length: '.strlen($params),
    'x-api-user: '.$x_username,
    'x-api-key: '.$x_apikey
));

// read api response
$res              = curl_exec($req);

// close curl
curl_close($req);

// print the raw json response
var_dump($res);
```
# Request Body Parameters
`name` - `[Type: String]` `[Required]` 

`phone` -	`[Type: String]` `[Required]` - Must be in international format.

`tags` - `[Type: String]`	`[Optional]` - A unique field to help group contacts e.g football,team,family.

`groups` - `[Type: String]`	`[Optional]` - This is a group name that the contacts will be added to. It must be an existing group.
# Response Body Parameters
## Response in case of successful editing of a contact:
```json
{
    "status": 200,
    "message": "Contact has been updated"
}
```
# Onehub Fetch Contacts PHP library
```PHP
// authentication
$x_username          = "";
$x_apikey            = "";

// endoint
$fetchContactURL     = "https://api.braceafrica.com/v1/contacts/fetch";

// encoding params
$req                 = curl_init($fetchContactURL);

curl_setopt($req, CURLOPT_CUSTOMREQUEST, "GET");
curl_setopt($req, CURLOPT_TIMEOUT, 60);
curl_setopt($req, CURLOPT_SSL_VERIFYPEER, FALSE);
curl_setopt($req, CURLOPT_RETURNTRANSFER, true);
curl_setopt($req, CURLOPT_HTTPHEADER, array(
    'Content-Type: application/json',
    'x-api-user: '.$x_username,
    'x-api-key: '.$x_apikey
));

// read api response
$res              = curl_exec($req);

// close curl
curl_close($req);

// print the raw json response
var_dump($res);
```
# Request Body Parameters
`name` - `[Type: String]` `[Required]` 

`phone` -	`[Type: String]` `[Required]` - Must be in international format.

`tags` - `[Type: String]`	`[Optional]` - A unique field to help group contacts e.g football,team,family.

`groups` - `[Type: String]`	`[Optional]` - This is a group name that the contacts will be added to. It must be an existing group.
# Response Body Parameters
## Response in case of successful fetching of a contact:
```json
{
    "status": 200,
    "contacts": [
        {
            "id": 2,
            "name": "Jane Mwaura",
            "phoneNumber": "+254712345678",
            "tags": "kenya,nairobi",
            "groups": [],
            "createdOn": "2019-12-02T00:00:00.000Z",
            "lastEditedOn": null
        }
    ]
}
```
# Onehub Delete Contacts PHP library
```PHP
// authentication
$x_username           = "";
$x_apikey             = "";

// id of contact to delete
$params            = array(
    "contactIds"=>array(1,2,3,4),
);

$contactsData = json_encode($params);

// endoint
$deleteContactURL     = "https://api.braceafrica.com/v1/contacts/delete;

$req                  = curl_init($deleteContactURL);

curl_setopt($req, CURLOPT_CUSTOMREQUEST, "POST");
curl_setopt($req, CURLOPT_TIMEOUT, 60);
curl_setopt($req, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($req, CURLOPT_RETURNTRANSFER, true);
curl_setopt($req, CURLOPT_POSTFIELDS, $contactsData);
curl_setopt($req, CURLOPT_HTTPHEADER, array(
    'Content-Type: application/json',
    'x-api-user: '.$x_username,
    'x-api-key: '.$x_apikey
));

// read api response
$res              = curl_exec($req);

// close curl
curl_close($req);

// print the raw json response
var_dump($res);
```
## ```!``` Please note that this will also remove the contact from all linked groups.
```json
{
    "contactIds": [1,2,3,4]
}
```
# Request Body Parameters
`name` - `[Type: String]` `[Required]` 

`phone` -	`[Type: String]` `[Required]` - Must be in international format.

`tags` - `[Type: String]`	`[Optional]` - A unique field to help group contacts e.g football,team,family.

`groups` - `[Type: String]`	`[Optional]` - This is a group name that the contacts will be added to. It must be an existing group.
# Onehub PHP Create Group Library
```PHP
// authentication
$x_username           = "";
$x_apikey             = "";

// id of contact to delete
$params = array(
    "name" => "",
    "tags" => "",
);

$addGroup = json_encode($params);

// endoint
$addGroupURL     = "https://api.braceafrica.com/v1/contacts/groups/add";

$req             = curl_init($addGroupURL);

curl_setopt($req, CURLOPT_CUSTOMREQUEST, "POST");
curl_setopt($req, CURLOPT_TIMEOUT, 60);
curl_setopt($req, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($req, CURLOPT_RETURNTRANSFER, true);
curl_setopt($req, CURLOPT_POSTFIELDS, $addGroup);
curl_setopt($req, CURLOPT_HTTPHEADER, array(
    'Content-Type: application/json',
    'x-api-user: '.$x_username,
    'x-api-key: '.$x_apikey
));

// read api response
$res              = curl_exec($req);

// close curl
curl_close($req);

// print the raw json response
var_dump($res);
```
# Request Body Parameters
`name` - `[Type: String]` `[Required]` - The group name.

`tags` - `[Type: String]`	`[Optional]` - These are tags in the contacts you want to link. The group will be formed and the contacts automatically linked to the group.
# Onehub PHP Edit Group Library
```PHP
// authentication
$x_username           = "";
$x_apikey             = "";

$groupId = "";

// id of contact to delete
$params = array(
    "name"=>""
);

$editGroup = json_encode($params);

// endoint
$editGroupURL     = "https://api.braceafrica.com/v1/contacts/groups/edit/".$groupId;

$req                  = curl_init($editGroupURL);

curl_setopt($req, CURLOPT_CUSTOMREQUEST, "POST");
curl_setopt($req, CURLOPT_TIMEOUT, 60);
curl_setopt($req, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($req, CURLOPT_RETURNTRANSFER, true);
curl_setopt($req, CURLOPT_POSTFIELDS, $editGroup);
curl_setopt($req, CURLOPT_HTTPHEADER, array(
    'Content-Type: application/json',
    'x-api-user: '.$x_username,
    'x-api-key: '.$x_apikey
));

// read api response
$res              = curl_exec($req);

// close curl
curl_close($req);

// print the raw json response
var_dump($res);
```
# Request Body Parameters
`name` - `[Type: String]` `[Required]` - The group name.

`tags` - `[Type: String]`	`[Optional]` - These are tags in the contacts you want to link. The group will be formed and the contacts automatically linked to the group.
# Response Body Parameters
## Response in case of successful editing of a group:
```json
{
    "status": 200,
    "message": "Group has been updated"
}
```
# Onehub PHP Fetch Group Library
```PHP
// authentication
$x_username           = "";
$x_apikey             = "";

// endoint
$fetchGroupsURL       = "https://api.braceafrica.com/v1/contacts/groups/fetch";

$req                  = curl_init($fetchGroupsURL);

curl_setopt($req, CURLOPT_CUSTOMREQUEST, "GET");
curl_setopt($req, CURLOPT_TIMEOUT, 60);
curl_setopt($req, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($req, CURLOPT_RETURNTRANSFER, true);
curl_setopt($req, CURLOPT_HTTPHEADER, array(
    'Content-Type: application/json',
    'x-api-user: '.$x_username,
    'x-api-key: '.$x_apikey
));

// read api response
$res              = curl_exec($req);

// close curl
curl_close($req);

// print the raw json response
var_dump($res);
```
# Request Body Parameters
`name` - `[Type: String]` `[Required]` - The group name.

`tags` - `[Type: String]`	`[Optional]` - These are tags in the contacts you want to link. The group will be formed and the contacts automatically linked to the group.
# Response Body Parameters
## Response in case of successful fetching of a group:
```json
{
    "status": 200,
    "groups": [
        {
            "groupId": 12,
            "groupName": "Kenzu Safaris",
            "createdOn": "2019-05-17T00:00:00.000Z",
            "contacts": []
        }
    ]
}
```
# Onehub PHP Link Contacts To Group Library
```PHP
// authentication
$x_username           = "";
$x_apikey             = "";

$groupId = "";

// id of contact to delete
$params = array(
    "contactIds"=>array(1,2,3,4),
);

$contactsData = json_encode($params);

// endoint
$addContactsToGroupURL     = "https://api.braceafrica.com/v1/contacts/add/".$groupId;

$req                  = curl_init($addContactsToGroupURL);

curl_setopt($req, CURLOPT_CUSTOMREQUEST, "POST");
curl_setopt($req, CURLOPT_TIMEOUT, 60);
curl_setopt($req, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($req, CURLOPT_RETURNTRANSFER, true);
curl_setopt($req, CURLOPT_POSTFIELDS, $contactsData);
curl_setopt($req, CURLOPT_HTTPHEADER, array(
    'Content-Type: application/json',
    'x-api-user: '.$x_username,
    'x-api-key: '.$x_apikey
));

// read api response
$res              = curl_exec($req);

// close curl
curl_close($req);

// print the raw json response
var_dump($res);
```
# Request Body Parameters
`name` - `[Type: String]` `[Required]` - The group name.

`tags` - `[Type: String]`	`[Optional]` - These are tags in the contacts you want to link. The group will be formed and the contacts automatically linked to the group.
# Response Body Parameters
## Response in case of successful linking contacts to a group:
```json
{
    "status": 200,
    "message": "The contacts linked to group"
}
```
# Onehub PHP Fetch Group Contacts Library
```PHP
// authentication
$x_username           = "";
$x_apikey             = "";

$groupId = "";

// endoint
$fetchGroupContactsURL       = "https://api.braceafrica.com/v1/contacts//groups/fetch/".$groupId;

$req                  = curl_init($fetchGroupContactsURL);

curl_setopt($req, CURLOPT_CUSTOMREQUEST, "GET");
curl_setopt($req, CURLOPT_TIMEOUT, 60);
curl_setopt($req, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($req, CURLOPT_RETURNTRANSFER, true);
curl_setopt($req, CURLOPT_HTTPHEADER, array(
    'Content-Type: application/json',
    'x-api-user: '.$x_username,
    'x-api-key: '.$x_apikey
));

// read api response
$res              = curl_exec($req);

// close curl
curl_close($req);

// print the raw json response
var_dump($res);
```
# Request Body Parameters
`name` - `[Type: String]` `[Required]` - The group name.

`tags` - `[Type: String]`	`[Optional]` - These are tags in the contacts you want to link. The group will be formed and the contacts automatically linked to the group.
# Response Body Parameters
## Response in case of successful fetching group contacts:
```json
{
    "groupId": 2536,
    "groupName": "Chama Ya Mama",
    "contacts": [
        {
            "id": 65,
            "name": "John Doe",
            "phoneNumber": "+2547xxx4578",
            "tags": "chairman"
        },
        {
            "id": 63,
            "name": "Pendo JM",
            "phoneNumber": "+2547xxy4597",
            "tags": "member"
        }
    ]
}
```
# Onehub PHP Remove Group Contacts Library
```PHP
// authentication
$x_username           = "";
$x_apikey             = "";

$groupId = "";

// id of contact to delete
$params = array(
    "contactIds"=>array(1,2,3,4),
);

$contactsData = json_encode($params);

// endoint
$deleteGroupContactsURL     = "https://api.braceafrica.com/v1/contacts/delete/".$groupId;

$req                  = curl_init($deleteGroupContactsURL);

curl_setopt($req, CURLOPT_CUSTOMREQUEST, "POST");
curl_setopt($req, CURLOPT_TIMEOUT, 60);
curl_setopt($req, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($req, CURLOPT_RETURNTRANSFER, true);
curl_setopt($req, CURLOPT_POSTFIELDS, $contactsData);
curl_setopt($req, CURLOPT_HTTPHEADER, array(
    'Content-Type: application/json',
    'x-api-user: '.$x_username,
    'x-api-key: '.$x_apikey
));

// read api response
$res              = curl_exec($req);

// close curl
curl_close($req);

// print the raw json response
var_dump($res);
```
# Request Body Parameters
`name` - `[Type: String]` `[Required]` - The group name.

`tags` - `[Type: String]`	`[Optional]` - These are tags in the contacts you want to link. The group will be formed and the contacts automatically linked to the group.
# Response Body Parameters
## Response in case of successful removing group contacts:
```json
{
    "status": 200,
    "message": "Contacts removed form group"
}
```
# Onehub PHP Delete Groups Library
```PHP
// authentication
$x_username           = "";
$x_apikey             = "";

// id of group to delete
$groupId = "";

// endoint
$deleteGroupURL             = "https://api.braceafrica.com/v1/contacts/groups/delete";

$params = array(
    "groupIds"=>array(1,2,3,4)
);

$deleteGroups = json_encode($params)

$req                  = curl_init($deleteGroupURL);

curl_setopt($req, CURLOPT_CUSTOMREQUEST, "POST");
curl_setopt($req, CURLOPT_TIMEOUT, 60);
curl_setopt($req, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($req, CURLOPT_POSTFIELDS, $deleteGroups);
curl_setopt($req, CURLOPT_RETURNTRANSFER, true);
curl_setopt($req, CURLOPT_HTTPHEADER, array(
    'Content-Type: application/json',
    'x-api-user: '.$x_username,
    'x-api-key: '.$x_apikey
));

// read api response
$res              = curl_exec($req);

// close curl
curl_close($req);

// print the raw json response
var_dump($res);
```
# Request Body Parameters
`name` - `[Type: String]` `[Required]` - The group name.

`tags` - `[Type: String]`	`[Optional]` - These are tags in the contacts you want to link. The group will be formed and the contacts automatically linked to the group.
# Response Body Parameters
## Response in case of successful deleting groups:
```json
{
    "status": 200,
    "message": "4 groups have been deleted"
}
```
# Onehub PHP Sender Ids Library
```PHP
// authentication
$x_username           = "";
$x_apikey             = "";

// endoint
$fetchSenderidsURL     = "https://api.braceafrica.com/v1/sms/senderIds/fetch";

$req                  = curl_init($fetchSenderidsURL);

curl_setopt($req, CURLOPT_CUSTOMREQUEST, "GET");
curl_setopt($req, CURLOPT_TIMEOUT, 60);
curl_setopt($req, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($req, CURLOPT_RETURNTRANSFER, true);
curl_setopt($req, CURLOPT_HTTPHEADER, array(
    'Content-Type: application/json',
    'x-api-user: '.$x_username,
    'x-api-key: '.$x_apikey
));

// read api response
$res              = curl_exec($req);

// close curl
curl_close($req);

// print the raw json response
var_dump($res);
```
# Response Body Parameters
## Response in case of successful fetching of Sender Ids:
```json
{
    "status": 200,
    "senderids": [
        {
            "sender_id": "BraceAfrica",
            "country": "Kenya",
            "status": "active"
        },
        {
            "sender_id": "JubaPay",
            "country": "Kenya",
            "status": "active"
        },
        {
            "sender_id": "Foleni",
            "country": "Uganda",
            "status": "active"
        }
    ]
}
```
# Onehub PHP Fetch Account Balance Library
```PHP
// authentication
$x_username           = "";
$x_apikey             = "";

// endoint
$fetchBalanceURL     = "https://api.braceafrica.com/v1/billing/balance";

$req                  = curl_init($fetchBalanceURL);

curl_setopt($req, CURLOPT_CUSTOMREQUEST, "GET");
curl_setopt($req, CURLOPT_TIMEOUT, 60);
curl_setopt($req, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($req, CURLOPT_RETURNTRANSFER, true);
curl_setopt($req, CURLOPT_HTTPHEADER, array(
    'Content-Type: application/json',
    'x-api-user: '.$x_username,
    'x-api-key: '.$x_apikey
));

// read api response
$res              = curl_exec($req);

// close curl
curl_close($req);

// print the raw json response
var_dump($res);
```
# Response Body Parameters
## Response in case of successful fetching account balance:
```json
{
    "status": 200,
    "data": {
        "amount": 6080.11,
        "currency": "KES"
    }
}
```
# Onehub PHP Fetch Account Statement Library
```PHP
// authentication
$x_username           = "";
$x_apikey             = "";

// endoint
$fetchStatementURL     = "https://api.braceafrica.com/v1/billing/topups";

$req                  = curl_init($fetchStatementURL);

curl_setopt($req, CURLOPT_CUSTOMREQUEST, "GET");
curl_setopt($req, CURLOPT_TIMEOUT, 60);
curl_setopt($req, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($req, CURLOPT_RETURNTRANSFER, true);
curl_setopt($req, CURLOPT_HTTPHEADER, array(
    'Content-Type: application/json',
    'x-api-user: '.$x_username,
    'x-api-key: '.$x_apikey
));

// read api response
$res              = curl_exec($req);

// close curl
curl_close($req);

// print the raw json response
var_dump($res);
```
# Response Body Parameters
## Response in case of successful fetching account statement:
```json
{
    "status": 200,
    "data": [
        {
            "id": 4155,
            "amount": "KES 500",
            "description": "Mpesa Code ML689276",
            "type": "MPESA",
            "date_created": "2019-12-22T14:38:44.000Z",
            "currency": "KES"
        }
        {
            "id": 4338,
            "amount": "KES 1100",
            "description": "Mpesa Code MJUYEO67M",
            "type": "MPESA",
            "date_created": "2019-12-22T14:38:44.000Z",
            "currency": "KES"
        }
        {
            "id": 4598,
            "amount": "KES 8000",
            "description": "Admin Top Up",
            "type": "Admin",
            "date_created": "2019-12-22T14:38:44.000Z",
            "currency": "KES"
        }
    ]
}
```
