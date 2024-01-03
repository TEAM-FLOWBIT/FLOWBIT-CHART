# SVG Chart Library(Flowbit)
## About
This library is a tool that utilizes SVG to draw line charts based on the data prepared by the user.

[Demo](https://frontserver.apps.sys.paas-ta-dev10.kr/)
## How to use
1. **Click green `<> Code` Button and clone this repository!**
2. **Import and render the chart**
```js
 let arr = [
      49240292.0, 49959348.0, 49415788.0, 49089796.0, 49993528.0, 50756712.0,
      50458944.0, 49985408.0, 49682928.0,
  ];

  let arr2 = [
      49788000, 49218000, 49025000, 49779000, 50595000, 50429000, 50021000,
      49536000, 50064000, 50692000, 50479000, 
  ];

  let labels = [
	'1','2','3','4','5','6','7','8','9'
  ];

  let arrMax = Math.max(...arr);
  let arrMin = Math.min(...arr);
  let arr2Max = Math.max(...arr);
  let arr2Min = Math.min(...arr);
  
  const dataList = [
      {
        label: 'BTC 실제가격',
        color: '#fff',
        width: 3,
        data: arr2,
        min: arr2Min,
        max: arr2Max,
      },
      {
        label: 'BTC 예측가격',
        color: '#79ffe1',
        width: 4,
        data: arr,
        min: arrMin,
        max: arrMax,
      },

    ];
   
   let chart = new Chart({
      targetId: 'chart', // The ID value of the parent HTML element where the chart will be generated.
      size: {            // Size of Chart
        width: 1500, 
        height: 790, 
        font: 15,    
      },
      datas: dataList,   // The datas to display on the screen through the chart.
      labels: labels,    // The labels appearing on the x-axis of the chart.
      backgroundColor: 'rgba(37, 57, 88, 0.35)', // The background color of chart
      hoverCardBackgroundColor: // The background color of the card that appears when hovering over the chart.
        'linear-gradient(107deg, rgba(250, 0, 255, 0.48) -36.41%, rgba(72, 81, 155, 0.78) 75.37%)',
    });
```

If you want to use the zoom in/out feature, you can add the following code.

```js
 let chart = new Chart({
      targetId: 'chart',
      size: {
        width: 1500,
        height: 790,
        font: 15,
      },
      datas: dataList,
      labels: labels,
      backgroundColor: 'rgba(37, 57, 88, 0.35)',
      hoverCardBackgroundColor:
        'linear-gradient(107deg, rgba(250, 0, 255, 0.48) -36.41%, rgba(72, 81, 155, 0.78) 75.37%)',
      zoom: true, // zoom mode
      showDataCount: 3, // The number of datas to display initially on the screen.
      showLabelCount: 3, // The fixed number of labels to display on the screen consistently.
    });
```

If you want to apply gradient colors, you can add the following code.
You need to create gradients directly using the SVG `<defs>` tag.
```js
 const dataList = [
...
      {
        label: 'BTC 예측가격',
        customColor: (create) => {
          let ns = 'http://www.w3.org/2000/svg';
          
          // line
          const linearGradientTag = document.createElementNS(
            ns,
            'linearGradient'
          );

          const linearStop1 = document.createElementNS(ns, 'stop');
          linearStop1.setAttribute('stop-color', '#FA00FF');

          const linearStop2 = document.createElementNS(ns, 'stop');
          linearStop2.setAttribute('offset', '1');
          linearStop2.setAttribute('stop-color', '#0085FF');
          
          linearGradientTag.appendChild(linearStop1);
          linearGradientTag.appendChild(linearStop2);

          // legend
          const LegendGradientTag = document.createElementNS(
            ns,
            'linearGradient'
          );

          const legendStop1 = document.createElementNS(ns, 'stop');
          legendStop1.setAttribute('stop-color', '#FA00FF');

          const legendStop2 = document.createElementNS(ns, 'stop');
          legendStop2.setAttribute('offset', '1');
          legendStop2.setAttribute('stop-color', '#0085FF');

          LegendGradientTag.appendChild(legendStop1);
          LegendGradientTag.appendChild(legendStop2);

          // circle
          const radialGradientTag = document.createElementNS(
            ns,
            'radialGradient'
          );

          const radialStop1 = document.createElementNS(ns, 'stop');
          radialStop1.setAttribute('offset', '.3');
          radialStop1.setAttribute('stop-color', '#FA00FF');

          const radialStop2 = document.createElementNS(ns, 'stop');
          radialStop2.setAttribute('offset', '1');
          radialStop2.setAttribute('stop-opacity', '0');
          radialStop2.setAttribute('stop-color', '#FA00FF');

          radialGradientTag.appendChild(radialStop1);
          radialGradientTag.appendChild(radialStop2);

          return {
            border: linearGradientTag,
            lastPoint: radialGradientTag,
            legend: LegendGradientTag,
          };
        },
        width: 4,
        data: arr,
        min: testMin,
        max: testMax,
      },
...
    ];
```
## Authors
  - [Always0ne](https://github.com/Always0ne) - **Dong gyun Yang** - <ehdrbdndns@naver.com>
