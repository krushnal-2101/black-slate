/*$Id$*/
(function() {
    if("undefined" === typeof(ZSMsgbar)){
        var ZSMsgbar = {};
        window.ZSMsgbar = ZSMsgbar;

        ZSMsgbar.removeBanner = function(){
            var element = document.getElementById('zsmsg-policy');
            element.parentNode.removeChild(element);
            localStorage.setItem("cookie_policy_accepted",true);        // NO I18N
        }

        function getThemeClass(){
            var messagebar_theme = message_bar_info.messagebar_theme;
            if(typeof messagebar_theme != "undefined"){
                if(messagebar_theme && messagebar_theme == "1"){
                    return "zpdark-section zpdark-section-bg";              // NO I18N
                }else if(messagebar_theme && messagebar_theme == "2"){
                    return "zplight-section zplight-section-bg";            // NO I18N
                }
            }else{
                return "zpdark-section zpdark-section-bg";              // NO I18N
            }
        }

        function checkIfContentChanged(mb_last_updated_time_local){
            var value = localStorage.getItem("cookie_policy_accepted"); // NO I18N
            if(mb_last_updated_time_local){
                if((parseFloat(mb_last_updated_time_local) >= message_bar_info.mb_last_updated_time) && (value === 'true')){
                    return false;
                }else{
                    return true;
                }
            }else{
                return true;
            }
        }

        function encodeHtmlEntities(str) {
            return str.replace(/&/g,'&amp;')
            .replace(/</g,'&lt;')
            .replace(/>/g,'&gt;')
            .replace(/"/g,'&quot;')
            .replace(/`/g,'');
        }

        ZSMsgbar.addZohoBanner = function() {
            var canShowMessageBar = false;
            
            var mb_last_updated_time_local = localStorage.getItem("mb_last_updated_time");      // NO I18N
            if(!mb_last_updated_time_local || checkIfContentChanged(mb_last_updated_time_local)){
                localStorage.setItem("mb_last_updated_time",message_bar_info.mb_last_updated_time);              // NO I18N
                canShowMessageBar = true;
                localStorage.setItem("cookie_policy_accepted",false);                               // NO I18N
            }

            if(canShowMessageBar){
                var message_bar_position_str;
                if(message_bar_info.message_bar_position == "2"){
                    message_bar_position_str = "bottom";       // NO I18N
                }else{
                    message_bar_position_str = "top";        // NO I18N
                }
                var addiv = document.createElement("div");
                addiv.id = "zsmsg-policy";
                var link_style = "zpbutton-wrapper zpbutton zpbutton-type-primary zpbutton-size-sm zpbutton-style-none";            // NO I18N
                addiv.innerHTML = "<div class=\""+getThemeClass()+"\" style=\"text-align: center;padding:12px 15px;"+                   // NO I18N
                                    "box-shadow: 0 0px 5px 1px #d6d6d6;position:fixed;"+message_bar_position_str+":0;left:0;width:100%;min-height:60px;z-index:1000001\">"+message_bar_info.message_bar_content.trim()+           // NO I18N
                                        "    <a class=\""+link_style+" \" href=\"javascript:;\" onclick=\"return ZSMsgbar.removeBanner();\" style=\"padding: 3px 10px;margin-left: 8px;\">"+encodeHtmlEntities(message_bar_info.accept_button_text)+
                                            "</a></div>";

                document.body.append(addiv);
            }
        }
        if(document.readyState === "complete" || document.readyState === "loaded"){
            ZSMsgbar.addZohoBanner();
        }else{
            document.addEventListener("DOMContentLoaded", function(event){
                ZSMsgbar.addZohoBanner();
            });
        }
    }
}());
