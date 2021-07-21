(function() {
    var currentScript="currentScript",scripts=document.getElementsByTagName("script");currentScript in document||Object.defineProperty(document,currentScript,{get:function(){try{throw Error()}catch(c){var r,t=(/.*at [^\(]*\((.*):.+:.+\)$/gi.exec(c.stack)||[!1])[1];for(r in scripts)if(scripts[r].src==t||"interactive"==scripts[r].readyState)return scripts[r];return null}}});
    currentScript = document.currentScript;

    var iframeElement = null, bnDiv = null, bnScaleDiv = null, bnFixedDiv = null, width = 100, height = 100, iOS = false;

    createIframe();

    function createIframe() {
        var urlParams = getUrlParams();
        var clickTag = urlParams.bnTag || '', responsive = urlParams.responsive || 0;

        width = 450;
        height = 250;

        var srcUrl = "https://cdn.onlymega.com/ckrdiaxvs000anw3xif2itqyx/index.html";

        clickTag = (clickTag == 'bannernow')?'':clickTag;
        srcUrl += '?bnTag=' + clickTag;

        iframeElement = document.createElement('iframe');
        iframeElement.src = srcUrl;

        iframeElement.setAttribute("style", "max-width: none !important; max-height: none !important;");
        iframeElement.style.position = 'absolute';
        iframeElement.style.left = '0';
        iframeElement.style.top = '0';
        iframeElement.style.backgroundColor = 'transparent';
        iframeElement.style.border = 'none';
        iframeElement.style.width = width + 'px';
        iframeElement.style.height = height + 'px';

        iframeElement.setAttribute('frameborder', '0');
        iframeElement.setAttribute('scrolling', 'no');
        iframeElement.setAttribute('allowTransparency', 'true');

        bnDiv = document.createElement('div');
        bnScaleDiv = document.createElement('div');
        bnFixedDiv = document.createElement('div');

        if (currentScript && currentScript.parentNode && currentScript.parentNode.nodeName.toLowerCase() != 'head') {
            currentScript.parentNode.appendChild(bnDiv);
        } else {
            document.body.appendChild(bnDiv);
        }

        bnDiv.appendChild(bnScaleDiv);
        bnScaleDiv.appendChild(bnFixedDiv);
        bnFixedDiv.appendChild(iframeElement);

        bnDiv.style.position = 'relative';
        bnDiv.style.overflow = 'hidden';

        bnFixedDiv.style.width = width + 'px';
        bnFixedDiv.style.height = height + 'px';

        bnScaleDiv.style.width = width + 'px';
        bnScaleDiv.style.height = height + 'px';

        iOS = /iPad|iPhone|iPod/.test(navigator.userAgent) && !window.MSStream;
        if (responsive == 1) {
            bnDiv.style.width = '100%';
            onWindowResize({target: window});
            addListener(window, 'resize', onWindowResize);
        } else {
            bnDiv.style.width = width + 'px';
            bnDiv.style.height = height + 'px';
        }
    }

    function getUrlParams() {
        var params = {};
        var dirtyVars = currentScript.src.match(/(\?|\&)([^=]+)\=([^&]+)/gi);
        if (dirtyVars && dirtyVars.length > 0) {
        dirtyVars.forEach(function(candidate, index) {
        var pair = candidate.replace(/[&\\?]/, '').split('=');
        params[pair[ 0]] = pair[ 1];
        });
        }
        return params;
    }

    function onWindowResize(e) {
        if (iOS) {
            iframeElement.style.width = 10 + 'px';
            bnFixedDiv.style.width = 10 + 'px';
            bnScaleDiv.style.width = 10 + 'px';
            bnDiv.style.overflow = 'visible';
        }

        var ratio = bnDiv.offsetWidth / width,
        newH = height * ratio;

        if (iOS) {
            iframeElement.style.width = width + 'px';
            bnFixedDiv.style.width = width + 'px';
        }

        bnScaleDiv.style.transform = 'scale(' + ratio + ') translate3d(0px, 0px, 0px)';
        bnScaleDiv.style.transformOrigin = '0px 0px 0px';
        bnScaleDiv.style.width = bnDiv.offsetWidth + 'px';
        bnScaleDiv.style.height = newH + 'px';
        bnDiv.style.height = newH + 'px';
        bnDiv.style.overflow = 'hidden';
    }

    function addListener(element, event, handler) {
        if (element.addEventListener) {
        element.addEventListener(event, handler, false);
        } else if (element.attachEvent) {
        element.attachEvent('on' + event, handler);
        } else {
        element[ 'on' + event] = handler;
        }
    }
})();
/* created=2021-07-21T13:13:29+00:00 cuid=ckrdiayaf001enw3xcnsra8yo */
