```
/**
 * AMD module: common utility
 * 
 * @Author: Hassan
 * Caution: do not modify code if you don't understand 'JavaScript Asynchronous Module Definition'
 */


define(['jquery', './ajax_helper', './message'], function($, AjaxHelper, Message){
	
	'use strict';
	
	const INPUT_MAX_LENGTH = 64;
	const JS_UNDEFINED = 'undefined';
	const AUTO_HIDE_TIME = 2000; // millisecond
	const MODAL_SHOW_DELAY_TIME = 100; // millisecond
	
	// modal feedback
	const FEEDBACK_DIV = ".feedback_div";
	const FEEDBACK_MSG_SPAN = ".feedback_msg";
	
	// RegExp literal, i = case insensitive, g = global (whole string)
	const PATTERN_ALPHANUMERIC = /[^A-Za-z0-9]+/ig; 
	const PATTERN_SYMBOL = /[^A-Za-z0-9!#()*,-.;<=>?@[^{|}~\]]+/ig;

	let common = {
			
		isEmpty : x => x == '',
		
		isZeroOrBelow : x => x <= 0,
		
		isMoreThanMax : x => x > INPUT_MAX_LENGTH,
		
		isInputOutOfRange : x => x > 64 || input < 8,
		
		isAlphanumeric : x => x.match(PATTERN_ALPHANUMERIC),
		
		isSymbol : x => x.match(PATTERN_SYMBOL),
		
		isUndef : x => typeof x === JS_UNDEFINED,
		
		isUndefOrEmpty : x => common.isUndef(x) || x === '',
		
		isNotUndefJquery : x => !common.isUndef(x.val()),
		
		hardReloadWindow : () => window.location.reload(true),
		
		delayedReload : () => {
			
			setTimeout(() => {
				
				common.hardReloadWindow();
				
			}, AUTO_HIDE_TIME);
		},
		
		delayAction: ({callback}) => {
			
			setTimeout(() => {
				
				callback();
				
			}, MODAL_SHOW_DELAY_TIME);
		},
		
		autoHide : $m => {
			setTimeout(function() {
				$m.modal('hide');
			}, AUTO_HIDE_TIME);
		},
		
		changeBGColor : ($div, isError) => {
			
			//console.log('changeBGColor => isError: ' + isError);
			if (isError) {
				if ($div.hasClass('feedback-success')) {
					//console.log('success => danger');
					$div.removeClass('feedback-success').addClass('feedback-danger');
				}
			} else {
				if ($div.hasClass('feedback-danger')) {
					//console.log('danger => success');
					$div.removeClass('feedback-danger').addClass('feedback-success');
				}
			}
		},
		
		fetchTimeZoneName : () => {
			let dtf = new Intl.DateTimeFormat();
			let timeZoneName = dtf.resolvedOptions().timeZone;
			return timeZoneName;
		},
		
		pad : x => x < 10 ? '0' + x : x,
				
		fetchTimezoneOffsetString : () => {
			
			let date = new Date();
			let sign = (date.getTimezoneOffset() > 0) ? "-" : "+";
			let offset = Math.abs(date.getTimezoneOffset());
			let hours = common.pad(Math.floor(offset / 60));
			let minutes = common.pad(offset % 60);
			
		    return sign + hours + ":" + minutes;
		},
		
		fetchTimeZoneOffSet : () => {
			let date = new Date();
			return date.getTimezoneOffset();
		},
		
		deleteCookie : (id, path) => {
			
			if(!id){
				id = 'JSESSIONID';
			}
			
			if(!path){
				path = '/mc';
			}
			
			Cookies.remove(id, { path: path });
			//console.log('attempted to delete cookie for ' + id);
			
			let cookey = Cookies.get(id);
			if(cookey){  // removeCookie did not work
				//console.log('removeCookie did not work => trying : Cookies.set');
				Cookies.set(id, '', { expires: -1, path: path });
			}
		},
		
		getContextPathWithSlash : () => {
			let ctxPath = $('meta[name="ctxPath"]').attr("content");
			if(!ctxPath){
				return '/';
			}
			return `${ctxPath}/`;
		},
		
		checkSessionValidity : ({onValid, onInvalid}) => {
			
			if(!onValid || !onInvalid){
				console.log('callback functions required');
				return;
			}
			
			AjaxHelper.FetchData({method: 'GET', uri: common.getContextPathWithSlash() + 'validity', dataType: 'json', callback: (response) => {
				
				if(response.message == 'parsererror'){ // if spring security redirects to login page while checking validity
					console.log(response.message);
					onInvalid(Message.errorSessionTimeout());
					return;
				}
				
				if(response.isError){
					console.log('Failed to check session validity');
					console.log('Cause: ' + response.message);
					return;
				}
				
				if(response.data.isValidSession){
					console.log(response.message);
					onValid();
				} else {
					console.log(response.message);
					onInvalid(Message.errorSessionTimeout());
				}
			}});
		},
		
		goToLoginPage : () => {
			let contextPathWithSlash = common.getContextPathWithSlash();
			window.location.href = contextPathWithSlash + 'login?invalidSession';
		},
		
		toggleActiveState: ($obj) => {

			$obj.prop('disabled', !$obj.is(':disabled'));
		},
		
		toggleVisibility: ($obj) => {
			
			if($obj.is(':visible')){
				$obj.hide();
			} else {
				$obj.show();
			}
		},
		toggleRedGreenColor: ($obj) => {
			
			if($obj.hasClass('btn-success')){
				
				$obj.removeClass('btn-success').addClass('btn-danger');
				
			} else {
				
				$obj.removeClass('btn-danger').addClass('btn-success');
			}

		},
		setFeedback : ({$modal, message, isError}) => {
			console.log('message:' + message);
			
			let $div = $modal.find(FEEDBACK_DIV);
			let $msg_span = $modal.find(FEEDBACK_MSG_SPAN);

			common.changeBGColor($div, isError);

			if (!message) {
				$msg_span.html('');
				$div.hide();
			} else {
				$msg_span.html(message);
				$div.show();
			}
		},
		onSessionInvalid : ({$modal, $actionButton, $cancelButton}) => {
			
			//common.toggleActiveState($actionButton); // activate button
			if($cancelButton){
				$cancelButton.hide(); // hide cancel button
			}
			
			common.toggleRedGreenColor($actionButton);
			$actionButton.text('Login');
			
			common.setFeedback({$modal: $modal, message: Message.errorSessionTimeout(), isError: true});
			
			//overwrite event
			$actionButton.off('click').on('click', function(e) {
				common.goToLoginPage();
			});
			
			$modal.on('hide.bs.modal', function(e) {
				$actionButton.trigger('click');
			});
		},
	}
	
	return common;
});
```
