<template>
  <div class="cp_bgpattern20">
    <div class="signup">
      <h1>新規アカウント登録</h1>
      <p class="explain">
        以下の項目を全て入力して「新規登録」ボタンをクリックしてください。
        <br />すでにアカウント登録をされている方は
        <router-link to="signin">こちらからログイン</router-link>できます。
      </p>
      <div id="errorMessage"></div>
      <form
        name="signup"
        id="signupform"
        action="https://hackfesfuk-api.azurewebsites.net/api/create-user"
        method="get"
      >
        <div class="signupform">
          <div id="errorMessage"></div>
          <p class="nameText">名前</p>
          <input type="text" class="textForm" name="name" size="22" maxlength="20" required />
          <p class="idText">学籍番号</p>
          <input type="text" class="textForm" name="number" size="22" maxlength="20" required />
          <p class="passText">パスワード</p>
          <input type="password" class="textForm" id="inpassword" size="22" maxlength="20" required />
          <p class="passText">パスワード(確認用)</p>
          <input
            type="password"
            class="textForm"
            id="checkpassword"
            size="22"
            maxlength="20"
            required
          />
          <input
            type="hidden"
            class="textForm"
            id="password"
            name="password"
            size="22"
            maxlength="20"
            required
          />
          <p>
            <input type="submit" class="buttonForm" id="signupButton" value="新規登録" />
          </p>
        </div>
      </form>
    </div>
  </div>
</template>
<script>
export default {
  mounted() {
    var submitButton = document.getElementById("signupform");
    submitButton.onsubmit=function() {
        /* 'inpassword' というid属性を持つ要素と 'checkpassword' というid属性を持つ要素を取得 */
        var input1 = document.getElementById("inpassword");
        var input2 = document.getElementById("checkpassword");
        // パスワードと再入力したパスワードが不一致なら
        if (input1.value != input2.value) {
          // エラー処理
          document.getElementById("errorMessage").innerHTML =
          "入力値にエラーがあります";
          return false;
        } else {
          // passwordというidを持つ要素にinpasswordの値を代入
          document.getElementById("password").value = input1.value;
          return true;
        }
      };
    // submitButton.addEventListener(
    //   "submit",
    //   function(event) {
    //     /* 'inpassword' というid属性を持つ要素と 'checkpassword' というid属性を持つ要素を取得 */
    //     var input1 = document.getElementById("inpassword");
    //     var input2 = document.getElementById("checkpassword");
    //     // パスワードと再入力したパスワードが不一致なら
    //     if (input1.value != input2.value) {
    //       // エラー処理
    //       document.getElementById("errorMessage").innerHTML =
    //       "入力値にエラーがあります";
    //       event.preventDefault();
    //       console.log("error");
    //     } else {
    //       // passwordというidを持つ要素にinpasswordの値を代入
    //       document.getElementById("password").value = input1.value;
    //       console.log("success");
    //     }
    //     while(1);
    //   },
    //   false
    // );
  }
};
</script>

<style>
/* 背景  */
.cp_bgpattern20 {
  background-color: rgba(250, 250, 250, 1);
  background-image: radial-gradient(
      closest-side,
      transparent 99.9%,
      rgba(236, 236, 236, 0.8) 100%
    ),
    radial-gradient(
      closest-side,
      transparent 99.9%,
      rgba(236, 236, 236, 0.8) 100%
    );
  background-position: 0 0, 30px 30px;
  background-size: 60px 60px;
  background-repeat: repeat;
  bottom: 0;
  height: 100%;
}

.explain {
  margin-top: 1em;
}

h1 {
  background: rgb(50, 120, 200); /*背景色*/
  padding: 0 0.5em; /*文字周りの余白*/
  color: rgb(230, 230, 230); /*文字を白に*/
  border-radius: 0.5em; /*角の丸み*/
}

.signupform {
  position: absolute;
  left: 50%;
  transform: translateX(-50%); /*  inputformの半分の大きさだけ左にずらす  */
  margin: 2em 1em;
  padding: 2em 1em;
  width: 300px;
  background-color: #fff; /* 背景色 */
  border: 1px solid #ccc; /* 枠線 */
  border-radius: 10px; /*角の丸み*/
  text-align: center;
}
.nameText,
.idText,
.passText {
  margin: 2em 0 0;
  text-align: left;
  white-space: pre-wrap;
}
.textForm {
  border: 1px solid #000;
}
.buttonForm {
  padding: 0.2em;
  margin: 1em 0 0;
  border: 1px solid #000;
  border-radius: 5px;
  text-align: center;
  background-color: #eee;
}
.signup {
  text-align: center;
}
</style>