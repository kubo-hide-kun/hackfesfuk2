<template>
    <div class="signin">
        <h1>ログイン</h1>
        <p>アカウントをお持ちでない方はこちらから<router-link to="signup">新規アカウント登録</router-link>をお願いします</p>
        <form name="signin" action="" method="get">
            <div class="inputform">
                <p class="idText">学籍番号</p>
                <input type="text" class="textForm" name="number" size="22" maxlength="20" required>
                <p class="passText">パスワード</p>
                <input type="text" class="textForm" name="password" size="22" maxlength="20" required>
                <p><input type="submit" class="buttonForm" name="loginButton" value="ログインする"></p>
            </div>
        </form>
    </div>
</template>

<style>
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