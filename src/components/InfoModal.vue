<script>
import { ref } from 'vue'

export default {
    
}

</script>

<template>
    <div class="modal-overlay" @click="$emit('close-modal')" >
        <div class="modal" @click.stop>
            <div class="modal-header">
                <h1>Info / 詳細</h1>
                <button class="close" @click="$emit('close-modal')" >X</button>
            </div>
            <div class="modal-body">
                <h2>Introduction / 紹介</h2>
                <p>This is a fanmade soundboard website for an indie vtuber, <a href="https://www.youtube.com/@KannagiTenri">Kannagi Tenri/巫てんり</a> by <a href="https://twitter.com/tuck161">Tuck Hoe</a> inspired by <a href="https://irysoundboard.com/">irysoundboard.com</a>.</p>
                <p>これは <a href="https://irysoundboard.com/">irysoundboard.com</a> にインスパイアされた <a href="https://twitter.com/tuck161">Tuck Hoe </a>による個人勢Vtuber <a href="https://www.youtube.com/@KannagiTenri">巫てんり</a>さんのファンメイド・サウンドボード・サイトです！</p>
                <h2>Credits / クレジット</h2>
                <ul>
                    <li>
                        <p>Background art is drawn by <a href="https://twitter.com/chilee79638443">chi lee</a>. Thanks for giving me permission to use it!</p>
                        <p>背景画像は<a href="https://twitter.com/chilee79638443">chi lee</a>によるものです。使用許可をありがとう！</p>
                    </li>
                    <li>
                        <p>Small images beside the title and on the buttons are membership emotes of <a href="https://www.youtube.com/@KannagiTenri">Kannagi Tenri/巫てんり</a>'s channel.</p>
                        <p>タイトルの横とボタンにある小さな画像は、<a href="https://www.youtube.com/@KannagiTenri">巫てんり</a>さんのチャンネルのメンバーエモートです。</p>
                    </li>
                </ul>
            </div>
            <div class="modal-body">
                <h5>If you want to suggest any sounds/voice of Tenri, please suggest it here <a href="https://forms.gle/VYrvfH6JExQge6AVA">https://forms.gle/VYrvfH6JExQge6AVA</a>. Thanks for your suggestions!</h5>
                <h5>てんりのサウンド／ボイスを提案したい方は、こちら<a href="https://forms.gle/VYrvfH6JExQge6AVA">（https://forms.gle/VYrvfH6JExQge6AVA）</a>から提案してください。ご提案ありがとうございました！</h5>
            </div>
        </div>
    </div>
</template>

<style scoped>

.modal h1{

    display: inline;
    padding-top: 20px;
}

</style>
