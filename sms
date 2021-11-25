  <!doctype html>
  <html lang="en">

  <head>
    <!-- Required meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css" rel="stylesheet">

    <title>SMS API TESTING</title>

    <style>
      .bg {
        background-image: url("bg.png");
        background-repeat: no-repeat;
        background-size: cover;
        height: 100vh;
      }

      .bg-2 {

        background: rgb(255 255 255 / 92%);
      }

      body {
        margin: 0;
        padding: 0;
        display: grid;
        place-content: center;
        min-height: 100vh;
      }

      #form_login {
        left: 50%;
        top: 40%;
        position: absolute;
        transform: translate(-50%, -50%);
      }
    </style>
  </head>

  <body class="bg">

    <div class="container">


      <?php
    if(isset($_SESSION["success"])){ ?>
      <div class="alert alert-warning alert-dismissible fade show" role="alert">
        <strong>Success</strong> Message Send Successful!
        <button type="button" class="btn-close" data-bs-dismiss="alert" aria-label="Close"></button>
      </div>

      <?php }
    unset($_SESSION["success"]);
    ?>

      <div class="row justify-content-center">
        <div class="col-md-6 col-lg-4 col-xl-3">
          <div class="" id="form_login">
            <h1 class="text-center fw-bold mb-3 text-white">SEND SMS FREE</h1>

            <form class="p-4  shadow rounded bg-2" action="" method="post">
              <div class="mb-3">

                <label for="phone" class="form-label">Phone Nubmer</label>
                <input type="text" class="form-control" id="phone" name="phone" required placeholder="01795-00000">
              </div>
              <div class="mb-3">
                <label for="msg" class="form-label">Your Message</label>
                <textarea class="form-control" id="sms_content" name="msg" rows="5" required> </textarea>
                <p class="pull-right charCount help-block font12">26 characters | 134 characters left | 1 SMS (160
                  Char./SMS)</p>
                <span class="help-block"></span>
              </div>
              <div class="text-center">
                <button type="submit" class="btn btn-dark">Submit</button>
              </div>

            </form>
          </div>
        </div>
      </div>
    </div>
    <?php
  session_start();
        $msg = $phone = "";
          
          if ($_SERVER["REQUEST_METHOD"] == "POST") {
            $phone = sendSMS($_POST["phone"]);
            $msg = sendSMS($_POST["msg"]);
      
  // API Key Like 6RMQ3D17T69t6961Q8FyQma1P77kxa1Ku3laV617
  
            $curl = curl_init();
            curl_setopt_array($curl, array(
              CURLOPT_URL => 'https://api.sms.net.bd/sendsms',
              CURLOPT_RETURNTRANSFER => true,
              CURLOPT_CUSTOMREQUEST => 'POST',
              CURLOPT_POSTFIELDS => array('api_key' => 'Your API Key','msg' => $msg,'to' => $phone),
            ));
            $response = curl_exec($curl);

            curl_close($curl); 
            
            if($response){
                $_SESSION["success"] = "Message Send Successful!";
            }
            
            header('Location: '.$_SERVER['PHP_SELF']);
            
          }
          
          
          function sendSMS($data) {
            $data = trim($data);
            $data = stripslashes($data);
            $data = htmlspecialchars($data);
            return $data;
          }
          


  ?>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>
    <script>
      $(document).ready(function () {

        $(document).on(
          'input change keyup propertychange paste',
          'textarea#sms_content',
          function () {
            let str = this.value.trim(),
              chars = str.length;
            let GSMC =
              '@Â£$Â¥Ã¨Ã©Ã¹Ã¬Ã²Ã‡\nÃ˜Ã¸\rÃ…Ã¥Î”_Î¦Î“Î›Î©Î Î¨Î£Î˜ÎžÃ†Ã¦ÃŸÃ‰ !"#Â¤%&\'()*+,-./0123456789:;<=>?Â¡ABCDEFGHIJKLMNOPQRSTUVWXYZÃ„Ã–Ã‘ÃœÂ§Â¿abcdefghijklmnopqrstuvwxyzÃ¤Ã¶Ã±Ã¼Ã ';
            let exGSMC = ['~', '^', '{', '}', '[', ']', '|', '\\', 'â‚¬'];
            let hasMoreThanAscii = [...str].some(
              (char) => !GSMC.includes(char) && !exGSMC.includes(char)
            );

            // if only gsm and has gsm ext characters chars++
            [...str].some(function (char) {
              !hasMoreThanAscii && exGSMC.includes(char) ? chars++ : false;
            });

            // normal sms
            let per_message = hasMoreThanAscii ? 70 : 160;

            // if multi sms
            if (chars > per_message) {
              per_message = hasMoreThanAscii ? 67 : 153;
            }

            let messages = Math.ceil(chars / per_message);
            let remaining = per_message * messages - chars;

            if (remaining === 0 && messages === 0) {
              remaining = per_message;
            }

            $('.charCount').html(
              `${chars} characters | ${remaining} characters left | ${messages} SMS (${per_message} Char./SMS)`
            );
          }
        );

      });
    </script>
  </body>

  </html>
