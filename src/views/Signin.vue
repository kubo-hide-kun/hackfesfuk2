<template>
    <div class="signin">
        <h1>This is an signin page</h1>
        <div class="inputform">
            <p>メールアドレス：<input type="text" name="mailAdress" size="30" maxlength="20"></p>
            <p>パスワード：<input type="text" name="password" size="30" maxlength="20"></p>
            <p><input type="button" name="loginButton" value="ログインする"></p>
        </div>
    </div>
</template>

<style>
.inputform{
    margin: 2em 1em;
    padding: 2em 1em;
    width: 50%;
    height: 100%;
    background-color: #eee; /* 背景色 */
    border: 1px solid #ccc; /* 枠線 */
    border-radius: 10px; /*角の丸み*/
    text-align: center;
}
.inputform p{
    
}
    
</style>