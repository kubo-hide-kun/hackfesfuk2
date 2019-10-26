<template>
    <div class="signup">
        <h1>新規アカウント登録</h1>
        <p>以下の項目を全て入力して「新規登録」ボタンをクリックしてください。<br>
        すでにアカウント登録をされている方は<a href="">こちらからログイン</a>できます。</p>
        <form name="signup" action="" method="post">
            <div class="signupform">
                <p class="nameText">名前</p>
                <input type="text" class="textForm" name="name" size="22" maxlength="20" required>
                <p class="idText">学籍番号</p>
                <input type="text" class="textForm" name="number" size="22" maxlength="20" required>
                <p class="passText">パスワード</p>
                <input type="text" class="textForm" name="password" size="22" maxlength="20" required>
                <p><input type="submit" class="buttonForm" name="signupButton" value="新規登録"></p>
            </div>
        </form>
    </div>
</template>

<style>
.signupform{
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
.nameText,.idText, .passText{
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
.signup{
    text-align: center;
}

</style>