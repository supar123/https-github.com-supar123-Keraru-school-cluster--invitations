# https-github.com-supar123-Keraru-school-cluster--invitations
manneen barnootaa Kilaastara Qaraaruu keessatti argaman hunda Adeemsa baruu fi barsiisuu hordoofuu waniin barbaaduuf  
Ragaalee manneen barnoota hunda bifa liinkiitin hordofuun 
barbaada
<!DOCTYPE html>
<html lang="om">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <title>Keraru School Cluster — Login</title>

  <script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>

  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      font-family: Arial, sans-serif;
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      padding: 20px;
      background: linear-gradient(135deg, #073b66, #1683b8);
    }

    .login-box {
      width: 100%;
      max-width: 430px;
      background: #fff;
      padding: 30px;
      border-radius: 20px;
      box-shadow: 0 15px 40px rgba(0,0,0,.25);
    }

    .logo {
      width: 80px;
      height: 80px;
      margin: 0 auto 15px;
      border-radius: 50%;
      background: #073b66;
      color: white;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 34px;
      font-weight: bold;
    }

    h1 {
      text-align: center;
      color: #073b66;
      font-size: 26px;
      margin-bottom: 8px;
    }

    .subtitle {
      text-align: center;
      color: #666;
      line-height: 1.5;
      margin-bottom: 25px;
    }

    label {
      display: block;
      font-weight: bold;
      color: #333;
      margin-bottom: 7px;
    }

    input {
      width: 100%;
      padding: 13px;
      margin-bottom: 17px;
      border: 1px solid #ccc;
      border-radius: 10px;
      font-size: 16px;
      outline: none;
    }

    input:focus {
      border-color: #1683b8;
      box-shadow: 0 0 0 3px rgba(22,131,184,.12);
    }

    button {
      width: 100%;
      padding: 14px;
      border: none;
      border-radius: 10px;
      background: #073b66;
      color: white;
      font-size: 16px;
      font-weight: bold;
      cursor: pointer;
    }

    button:hover {
      background: #1683b8;
    }

    button:disabled {
      opacity: .6;
      cursor: not-allowed;
    }

    .forgot {
      display: block;
      text-align: right;
      color: #1683b8;
      font-size: 14px;
      cursor: pointer;
      margin: -5px 0 15px;
    }

    .message {
      display: none;
      padding: 12px;
      border-radius: 8px;
      margin-bottom: 15px;
      font-size: 14px;
      line-height: 1.5;
    }

    .success {
      display: block;
      background: #e8f7ee;
      color: #176b38;
    }

    .error {
      display: block;
      background: #fdecec;
      color: #a02020;
    }

    .footer {
      text-align: center;
      color: #777;
      font-size: 13px;
      line-height: 1.6;
      margin-top: 25px;
    }

    @media (max-width: 480px) {
      .login-box {
        padding: 23px;
      }

      h1 {
        font-size: 23px;
      }
    }
  </style>
</head>

<body>

  <div class="login-box">

    <div class="logo">K</div>

    <h1>Keraru School Cluster</h1>

    <p class="subtitle">
      Sirna Hordoffii fi To'annoo<br>
      Manneen Barnootaa
    </p>

    <div id="message" class="message"></div>

    <form id="loginForm">

      <label for="email">Email</label>

      <input
        type="email"
        id="email"
        placeholder="Email keessan galchaa"
        required
        autocomplete="email"
      >

      <label for="password">Password</label>

      <input
        type="password"
        id="password"
        placeholder="Password keessan galchaa"
        required
        autocomplete="current-password"
      >

      <span class="forgot" id="forgotPassword">
        Password irraanfattee?
      </span>

      <button type="submit" id="loginButton">
        🔐 Seeni
      </button>

    </form>

    <div class="footer">
      Godina Harargee Lixaa — Aanaa Doobbaa<br>
      Keraru / Qaraaruu School Cluster
    </div>

  </div>


<script>

  /* ================================
     SUPABASE CONFIG
  ================================= */

  const SUPABASE_URL =
    "https://blwpuiannyditjsaghdn.supabase.co";

  const SUPABASE_KEY =
    "sb_publishable_hJanJxqPXpTnFv-GTtjNWg_ITFJe-D7";

  const supabaseClient =
    window.supabase.createClient(
      SUPABASE_URL,
      SUPABASE_KEY
    );


  /* ================================
     ELEMENTS
  ================================= */

  const loginForm =
    document.getElementById("loginForm");

  const loginButton =
    document.getElementById("loginButton");

  const forgotPassword =
    document.getElementById("forgotPassword");

  const message =
    document.getElementById("message");


  /* ================================
     MESSAGE
  ================================= */

  function showMessage(text, type) {

    message.textContent = text;

    message.className =
      "message " + type;

  }


  /* ================================
     CHECK SESSION
  ================================= */

  async function checkSession() {

    const {
      data: { session }
    } = await supabaseClient.auth.getSession();

    if (session) {

      window.location.href =
        "dashboard.html";

    }
  }

  checkSession();


  /* ================================
     LOGIN
  ================================= */

  loginForm.addEventListener(
    "submit",
    async function(event) {

      event.preventDefault();

      const email =
        document.getElementById("email")
          .value
          .trim();

      const password =
        document.getElementById("password")
          .value;


      if (!email || !password) {

        showMessage(
          "Email fi Password guutaa.",
          "error"
        );

        return;
      }


      loginButton.disabled = true;

      loginButton.textContent =
        "Seenaa jira...";


      const {
        data,
        error
      } =
      await supabaseClient.auth
        .signInWithPassword({
          email: email,
          password: password
        });


      if (error) {

        showMessage(
          "Login hin milkoofne: " +
          error.message,
          "error"
        );

        loginButton.disabled = false;

        loginButton.textContent =
          "🔐 Seeni";

        return;
      }


      if (data.session) {

        showMessage(
          "Milkaa'eera! Dashboarditti ce'aa...",
          "success"
        );

        setTimeout(function() {

          window.location.href =
            "dashboard.html";

        }, 700);

      }

    }
  );


  /* ================================
     PASSWORD RESET
  ================================= */

  forgotPassword.addEventListener(
    "click",
    async function() {

      const email =
        document.getElementById("email")
          .value
          .trim();


      if (!email) {

        showMessage(
          "Jalqaba Email keessan galchaa.",
          "error"
        );

        return;
      }


      const {
        error
      } =
      await supabaseClient.auth
        .resetPasswordForEmail(
          email,
          {
            redirectTo:
              window.location.origin +
              "/password.html"
          }
        );


      if (error) {

        showMessage(
          "Password reset hin milkoofne: " +
          error.message,
          "error"
        );

        return;
      }


      showMessage(
        "Link haaromsaa Password email keessanitti ergameera.",
        "success"
      );

    }
  );


  /* ================================
     AUTH STATE
  ================================= */

  supabaseClient.auth.onAuthStateChange(
    function(event, session) {

      if (
        event === "SIGNED_IN" &&
        session
      ) {

        window.location.href =
          "dashboard.html";

      }

    }
  );

</script>

</body>
</html>
