/*$Id$*/
var BrowserDetect = {
    init: function (options) {
        this.browser = this.getBrowser();
        this.version = this.getVersion();
        this.options = options;
        var browserDetectDisabled = sessionStorage.getItem("browserDetectDisabled");//NO I18N
        if(browserDetectDisabled == null){
            sessionStorage.setItem("browserDetectDisabled", 'false');//NO I18N
            browserDetectDisabled = 'false';//NO I18N
        }
        if(this.browser && (browserDetectDisabled === 'false') && this.options.required[this.browser.browserName] && (this.version < this.options.required[this.browser.browserName])){
            this.show();
            var closeButton = document.querySelector('.update-msg-close');//NO I18N
            if(closeButton){
                if(this.options.hide){
                    closeButton.addEventListener('click',BrowserDetect.hide);
                }else{
                    closeButton.style.display = 'none';
                }
            }
        }
    },
    getVersion: function(){
        var currentBrowserInfo = this.browser, versionIdentifierarray, regexString;
        if(currentBrowserInfo){
            if(currentBrowserInfo.isChromiumBased){
            var versionIdentifier = 'Chrome';//NO I18N
            return parseInt(navigator.userAgent.match(new RegExp('(?:'+versionIdentifier+')\/(\\d+(\\.?_?\\d+)+)', 'i'))[1]);
            }else{
                var versionIdentifier = currentBrowserInfo.versionIdentifier ? currentBrowserInfo.versionIdentifier : this.browser.browserName;
                if (versionIdentifier.indexOf(',') > -1) {
                    versionIdentifierarray = versionIdentifier.split(',');
                    for(var i=0;i<versionIdentifierarray.length;i++){
                        if(versionIdentifierarray[i] == 'MSIE' && currentBrowserInfo.agentInformation.indexOf('MSIE')){
                            regexString = '(?:'+versionIdentifierarray[i]+') (\\d+(\\.?_?\\d+)+)';
                        }else if(versionIdentifierarray[i] == 'rv' && currentBrowserInfo.agentInformation.indexOf('rv')){
                            regexString = '(?:'+versionIdentifierarray[i]+')\/(\\d+(\\.?_?\\d+)+)';
                        }
                    }
                }else{
                    regexString = '(?:'+versionIdentifier+')\/(\\d+(\\.?_?\\d+)+)';
                }
                return parseInt(currentBrowserInfo.agentInformation.match(new RegExp(regexString, 'i'))[1]);
            }
        }
    },
    getBrowser: function(){
        var browserslist = this.browsersList, currentBrowser=null;
        if (browserslist) {
            var userAgent;
            for(var i=0;i<browserslist.length;i++){
                userAgent = browserslist[i].agentInformation;
                if (userAgent && userAgent.indexOf(browserslist[i].agentIdentifier) != -1){
                    currentBrowser = browserslist[i];
                    break;
                }
            }
            return currentBrowser;
        }
    },
    show: function () {
        this.updateMessage = document.createElement("div");
        this.updateMessage.className += (" update-msg-container");//NO I18N
        var updateMessageClose = "";
        if(this.options.hide){
            updateMessageClose = '<span class="update-msg-close" style="position: absolute;right: 0;top: 0;width: 40px;height: 100%;z-index: 2299483701;display: flex;justify-content: center;align-items: center;cursor: pointer;"><span class="update-msg-close-cross-left" style="width: 60%;height: 2px;background: #2e2e2e;transform: rotate(45deg);position: absolute;top: 50%;left: 0;"></span><span class="update-msg-close-cross-right" style="width: 60%;height: 2px;background: #2e2e2e;transform: rotate(135deg);position: absolute;top: 50%;left: 0;"></span></span>';
        }
        if(typeof i18n != "undefined" && i18n.get('browser.update.message')){
            var updateMessagei18n = i18n.get('browser.update.message','<span class="browser-name" style="font-weight: bold;">'+ this.browser.browserName +'</span>');
        }else{
            var updateMessagei18n = 'You seem to be on an older version of <span class="browser-name" style="font-weight: bold;">'+ this.browser.browserName +'</span> . Change or update your browser for a better experience.';//NO I18N
        }
        this.updateMessage.style.cssText = 'display: flex;text-align:center;justify-content: center;align-items: center;position: fixed;top: 0;left: 0;width: 100%;padding: 12px 40px 12px 12px;z-index: 2299483700;background: #f3b921;color: #2e2e2e;box-shadow: 0 3px 5px RGBA(0, 0, 0, 0.12);font-family: system-ui, "Segoe UI", Roboto, Helvetica, Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol";font-size: 15px;'//NO I18N
        this.updateMessage.innerHTML = '<span class="update-msg">'+ updateMessagei18n +'</span>'+ updateMessageClose;
        document.body.appendChild(this.updateMessage);
    },
    hide: function () {
        var msgContainer = document.querySelector('.update-msg-container');//NO I18N
        sessionStorage.setItem("browserDetectDisabled", 'true');//NO I18N
        msgContainer.style.display = 'none';
    },
    browsersList:[
        {
            browserName: "Brave",//NO I18N
            agentIdentifier: "isBrave",//NO I18N
            agentInformation: window.navigator.brave ? window.navigator.brave.isBrave.name : "",
            isChromiumBased: true
        },
        {
            agentIdentifier: "OPR",//NO I18N
            browserName: "Opera",//NO I18N
            agentInformation: navigator.userAgent,
            versionIdentifier: "OPR",//NO I18N
            isChromiumBased: true
        },
        {
            agentIdentifier: "Ulaa",//NO I18N
            browserName: "Ulaa",//NO I18N
            agentInformation: navigator.userAgent,
            isChromiumBased: true
        },
        {
            agentIdentifier: "Trident",//NO I18N
            browserName: "MSIE",//NO I18N
            agentInformation: navigator.userAgent,
            versionIdentifier: "rv,MSIE"//NO I18N
        },
        {
            agentIdentifier: "Edg",//NO I18N
            browserName: "Edge",//NO I18N
            agentInformation: navigator.userAgent,
            versionIdentifier: "Edg",//NO I18N
            isChromiumBased: true
        },
        {
            agentIdentifier: "Firefox",//NO I18N
            browserName: "Firefox",//NO I18N
            agentInformation: navigator.userAgent
        },
        {
            agentIdentifier: "Chrome",//NO I18N
            browserName: "Chrome",//NO I18N
            agentInformation: navigator.userAgent
        },
        {
            agentIdentifier: "Apple",//NO I18N
            browserName: "Safari",//NO I18N
            agentInformation: navigator.userAgent,
            versionIdentifier: "Version"//NO I18N
        }
    ]
};
var browserUpdateOptions ={
    reminder: 0,
    required: {
        Chrome: 88,
        Firefox: 85,
        Safari: 14,
        MSIE: 11,
        Edge: 88,
        Ulaa: 88,
        Opera: 88,
        Brave: 88
    },
    hide: true
};
document.addEventListener("DOMContentLoaded", function(event) {
    BrowserDetect.init(browserUpdateOptions);
});
