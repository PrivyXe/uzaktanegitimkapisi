// ==UserScript==
// @name         Uzaktan Eğitim Kapısı Videolarını Otomatik Arka Planda İzle
// @namespace    https://uzaktanegitimkapisi.cbiko.gov.tr/
// @version      v1.0.1
// @description  Uzaktan Eğitim Kapısı Videolarını, Bilgisayara Dokunmadan, Arka Arkaya, Arka Planda Sessizce İzlemenizi Sağlar
// @edit         PrivyXe
// @homepage     https://uzaktanegitimkapisi.cbiko.gov.tr/
// @supportURL   https://uzaktanegitimkapisi.cbiko.gov.tr/
// @match        https://uzaktanegitimkapisi.cbiko.gov.tr/Egitimler/video*
// @match        https://uzaktanegitimkapisi.cbiko.gov.tr/Egitimler/Video*
// @icon         https://www.google.com/s2/favicons?sz=64&domain=gov.tr
// @grant        none
// @run-at       document-end
// @require      http://code.jquery.com/jquery-3.4.1.min.js
// @license      GPL-2.0-only
// @downloadURL  https://update.greasyfork.org/scripts/480955/Uzaktan%20E%C4%9Fitim%20Kap%C4%B1s%C4%B1%20videolar%C4%B1n%C4%B1%20otomatik%20arkaplanda%20izle.user.js
// @updateURL    https://update.greasyfork.org/scripts/480955/Uzaktan%20E%C4%9Fitim%20Kap%C4%B1s%C4%B1%20videolar%C4%B1n%C4%B1%20otomatik%20arkaplanda%20izle.meta.js
// ==/UserScript==

(function() {
    'use strict';

    $(document).ready(function() {
        // Video player'ını seçiyoruz
        var myPlayer = videojs.getPlayer('CbikoPl');

        // Eğer video başlatılmamışsa, otomatik olarak başlatıyoruz
        function startVideo() {
            if (myPlayer.paused()) {
                myPlayer.play();
            }
        }

        // Arka planda olsa bile video durmasın
        $(window).focus(function() {
            startVideo();
            document.title = "Uzaktan Eğitim Kapısı - Video Oynuyor";
        });

        $(window).blur(function() {
            startVideo(); // Video arka planda olsa bile oynatmaya devam et
            document.title = "Uzaktan Eğitim Kapısı - Arka Plan";
        });

        // Sayfa yüklenmeden önce video başlaması için bekleme yap
        var videoLoaded = false;
        var videoCheckInterval = setInterval(function() {
            if ($('#CbikoPl_html5_api').length > 0 && !videoLoaded) {
                videoLoaded = true;
                startVideo(); // Sayfa yüklenirse video hemen başlasın
                clearInterval(videoCheckInterval);
            }
        }, 500); // Her yarım saniyede bir kontrol eder

        // Videoyu arka planda oynatırken ses kontrolü
        var muteButton = $(".vjs-mute-control");
        if (muteButton.length) {
            muteButton.click(); // Ses açma
        }

        // Otomatik oynatmak için "Play" butonuna tıklama
        setInterval(function() {
            var AutoPlayButton = $('.vjs-big-play-button');
            if (AutoPlayButton.length) {
                AutoPlayButton.click(); // Oynatma butonuna tıkla
            }
        }, 1000); // 1 saniyede bir kontrol et

        // Sayfa yenilemesi işlemi (10 dakika)
        setInterval(function() {
            window.location.reload(true); // Sayfayı 10 dakikada bir yenile
        }, 600000); // 600000 milisaniye = 10 dakika
    });
})();
