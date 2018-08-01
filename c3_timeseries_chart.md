```
/**
 * @Module: c3 timeseries chart
 * 
 * @Author: Hassan Md Tareq
 *
 * Module to draw timeseries line charts using c3.js
 */

define(["d3", "c3"], function(d3, c3){
	
	'use strict';

	// constants
	const INCOMING_TIME_FORMAT = '%Q'; // '%Q' => timestamp in milliseconds
	// Note: for type: 'timeseries' (X_AXIS_SETTING) xFormat: INCOMING_TIME_FORMAT might be ignored

	// axis setting
	let X_AXIS_SETTING = {
	  type: 'timeseries',
	  tick: {
		fit: true,
		format: "%Y-%m-%d",
		rotate: 45
	  },
	  label: { text: 'Datetime', position: 'outer-center' },
	  //min: xMin,
	  //max: xMax,
	  //padding: { left: 0, right: 100 },
	  //height: 50
	};

	let Y_AXIS_SETTING = {
	  label: { text: 'Value', position: 'outer-middle' },
	  min: 0,
	  padding: { bottom: 0, top: 50 }
	};

	let LEGEND_SETTING = {
	  show: true,
	  position: 'inset',
	  inset: {
		anchor: 'top-right',
		x: 10,
		y: -10,
		step: 1
	  }
	};

	let GRID_SETTING = { x: { show: true }, y: { show: true } };

	let ts = {
		
		Chart: '',
		
		drawTSChartWithJsonData: ({
			DIV_ID,
			JSON_DATA,
			VALUE_KEYS,
			X_AXIS = 'datetime',
			LINE_TYPE = 'spline',
			Y_AXIS_LABEL = ''
		}) => {
			
			// required fields
			if( !(DIV_ID && JSON_DATA && VALUE_KEYS) ){
				console.log("one or more required fields absent");
				return;
			}
			
			if(Y_AXIS_LABEL){ // default is set in Y_AXIS_SETTING
				Y_AXIS_SETTING.label.text = Y_AXIS_LABEL;
			}
			
			// adjust x axis tick marks
			X_AXIS_SETTING.tick.count = JSON_DATA.length * 2;
			
			let chart = c3.generate({
				bindto: DIV_ID,
				data: {
				  xFormat: INCOMING_TIME_FORMAT,
				  type: LINE_TYPE,
				  x: X_AXIS,
				  json: JSON_DATA,
				  keys: { x: X_AXIS, value: VALUE_KEYS }
				},
				axis: { x: X_AXIS_SETTING, y: Y_AXIS_SETTING },
				legend: LEGEND_SETTING,
				grid: GRID_SETTING,
				padding: { right: 20 }
			});
			
			ts.Chart = chart;
		}
	};
	
	return ts;
});
```
