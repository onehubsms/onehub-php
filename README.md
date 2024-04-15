# Onehub PHP Library
```
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
