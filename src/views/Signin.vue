<template>
    <div class="cp_bgpattern20">
        <div class="signin">
            <h1>ログイン</h1>
            <p class="explain">アカウントをお持ちでない方はこちらから<router-link to="signup">新規アカウント登録</router-link>をお願いします</p>
            <form name="signin" action="https://hackfesfuk-api.azurewebsites.net/api/login" method="get">
                <div class="inputform">
                    <p class="idText">学籍番号</p>
                    <input type="text" class="textForm" name="number" size="22" maxlength="20" required>
                    <p class="passText">パスワード</p>
                    <input type="password" class="textForm" name="password" size="22" maxlength="20" required>
                    <p><input type="submit" class="buttonForm" name="loginButton" value="ログインする"></p>
                </div>
            </form>
        </div>
    </div>
</template>

<style>

 /* 背景  */
.cp_bgpattern20{
	background-color: rgba(250,250,250,1);
	background-image:radial-gradient(closest-side,transparent 99.9%, rgba(236,236,236,0.8) 100%),
    radial-gradient(closest-side,transparent 99.9%, rgba(236,236,236,0.8) 100%);
    background-position: 0 0, 30px 30px;
	background-size: 60px 60px;
    background-repeat: repeat;
    bottom:0;
    height:100%;
}

.explain{
   margin-top:1em;
}

h1 {
  background: rgb(50,120,200); /*背景色*/
  padding: 0 0.5em;/*文字周りの余白*/
  color: rgb(230,230,230);/*文字を白に*/
  border-radius: 0.5em;/*角の丸み*/
}

.inputform{
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
.idText, .passText{
    margin: 2em 0 0;
    text-align: left;
    white-space: pre-wrap;
}


.textForm{
    border: 1px solid #000;
}

.buttonForm{
    padding: 0.2em;
    margin: 1em 0 0;
    border: 1px solid #000;
    border-radius: 5px;
    text-align: center;
    background-color: #eee;
}

.signin{
    text-align: center;
}

</style>