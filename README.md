# Joomla-K2
This is an Fixed issue of Joomla K2 Component and some improve it<br>
//By Abdulaziz Mierza<br>
//-------------------------------------------------------------------------//
1-Fixed issue with  Google reCAPTCHA v2 (28-4-2016)
2-Support Joomla Selection Language for  Google reCAPTCHA v2 (28-4-2016)
//------------------------------------------------------------------------//

1-bug in reCAPTCHA v2 on release version of K2 which is :
After accept comment & reload page >> reCAPTCHA not will shown
2-Add Suuport Joomla Language > for example if you using Germany language for joomla , its will show reCAPTCHA Germany from Google

PLease Replace these code in (Note this example only for comments, you can replace for other) :
[your joomla folder]/components/com_k2/views/item/view.html.php

FIND :
						if($params->get('recaptchaV2')) {
							$document->addScript('https://www.google.com/recaptcha/api.js?onload=onK2RecaptchaLoaded&render=explicit');
							$js = 'function onK2RecaptchaLoaded(){grecaptcha.render("recaptcha", {"sitekey" : "'.$item->params->get('recaptcha_public_key').'"});}';
							$document->addScriptDeclaration($js);
							$this->recaptchaClass = 'k2-recaptcha-v2';
						}


REPLACE WITH :
  						if($params->get('recaptchaV2')) {
							$document->addScript('https://www.google.com/recaptcha/api.js?hl=' . JFactory::getLanguage()
						->getTag() . '&onload=onK2RecaptchaLoaded&render=explicit');
							$js = 'function onK2RecaptchaLoaded(){grecaptcha.render("recaptcha", {"sitekey" : "'.$item->params->get('recaptcha_public_key').'"});}
							$K2(window).load(function() {
								onK2RecaptchaLoaded();
							});
							';
							$document->addScriptDeclaration($js);
							$this->recaptchaClass = 'k2-recaptcha-v2';
						}

NOTE :
YOU CAN USED FOR ANOTHER FILE LIKE : [your joomla folder]/plugins/system/k2/k2.php

You can download the PHP file (ONLY FOR [your joomla folder]/components/com_k2/views/item/view.html.php).
