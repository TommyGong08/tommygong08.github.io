---
layout: defaults/page
permalink: index.html
narrow: true
title: Welcome to Hailong's Personal Page
---

## About Me

{% include components/intro.md %}

[//]: # ([Here's the full feature list and some quick examples of what it can do.]&#40;{{ site.baseurl}}{% link _pages/about.md %}&#41;)

<br />

## Education Background

|         Year          |                                                                             Institute                                                                              | <img width=20/> Degree                              |
|:---------------------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:----------------------------------------------------|
|      2024.2-now       |  <img src="https://raw.githubusercontent.com/TommyGong08/tommygong08.github.io/refs/heads/main/_pages/doc/ANU_Logo.png" width=30/> Australian National University  | <img width=20/>M.S. Computing (Advanced)            |
|     2018.9-2022.6     | <img src="https://raw.githubusercontent.com/TommyGong08/tommygong08.github.io/refs/heads/main/_pages/doc/BIT_Logo.png" width=30/>  Beijing Institute of Technology | <img width=20/>B.S. Computer Science and Technology |

<br />

## Experience
- Research Student at ANU doing research on Photonic Computing (2024.12 - now)
- AOI Algorithmic Engineer at Shenzhen Yimeizhi Technology Co,.Ltd. (2023.3- 2023.12)
- Research Assistant at BIT supervised by [Prof. Jianwei Gong](https://me-english.bit.edu.cn/people/facultydept/vehiclee2/xs3/b125047.htm) and [Prof. Chao Lu](https://scholar.google.com/citations?user=0Jv8_7MAAAAJ&hl=zh-CN) ( 2022.7- 2023.1)
- Internship in ByteDance as Algorithm Engineer develop [Fastbot](https://github.com/bytedance/Fastbot_Android)( 2021.10-2022.3)
- Summer Research Internship with [Prof. Lili Su](https://lilisu3.sites.northeastern.edu/) on autonomous trajectory prediction (2021.7-2021.9)
- Autonomous System group of [BITFSD](http://www.bitfsd.com/) ( 2020-2022 )

<br />

### News
- **\[Dec.2025\]** Happy to share that I have been awarded the **Master of Computing (Advanced)** degree with **Commendation** from ANU, with an overall GPA of 6.67 / 7.0!
- **\[Nov.2025\]** Excited to share my master thesis work, **LightMat**, built on our team's photonic computing prototype ([video](https://drive.google.com/file/d/1GzqtUs4kAFqlLQIxayjiZsq-Vpm9nPbK/view))!
- **\[July.2025\]** I completed the third semester with two High Distinctions, resulting in a GPA of **7.0/7.0** and overall GPA of **6.56/7.0**!
- **\[April.2025\]**  I was invited to serve as a reviewer for *IEEE Transactions on Intelligent Transportation Systems (T-ITS)* and *IEEE Internet of Things Journal (IoT-J)*!
- **\[Dec.2024\]** I started the research project(thesis) under the supervision of [Dr. Amanda Barnard](https://comp.anu.edu.au/people/amanda-barnard/) and [Dr. Haibo Zhang](https://haibozhang-web.github.io/)! 
- **\[Nov.2024\]** I completed my second semester at ANU with two High Distinctions, one Distinction, resulting in a GPA of 6.67/7.0 and overall GPA of 6.43/7.0 in the first year!
- **\[June.2024\]** I completed my first semester at ANU with two High Distinctions, one Distinction, and one Credit, resulting in a GPA of 6.25/7.0!
- **\[Feb.2024\]** I start my Master of Computing(Advanced) studies at Australian National University, specializing in Computational Foundations!
- **\[Nov.2023\]** The paper about Multi-stream Information Fusion in Low-illumination Scenarios is accepted by IEEE T-ITS!
- **\[July.2023\]** Our research work on Online Risk Assessment for Human-robot Interaction is accepted by ITSC 2024!

[//]: # (- **\[Mar.2023\]** I join in Shenzhen Image Technology Co.,Ltd as full-time Algorithm Engineer, developing and optimizing algorithms for defect detection!)
<br />

### Contact
I am happy to share and discuss the previous projects, technology details and research interests with everybody, please feel free to drop me an [email](mailto:hailong.gong@anu.edu.au).
<hr />


<body data-article-id="homepage">  


<div class="page-views-container">
        <h6>Page Views</h6>
        <span id="page-views-today">Loading...</span>
        <span id="page-views">Loading...</span>
</div>

<br />

<h5> Visitors Map </h5>
<div id="mapid"></div>  
  
<script src="https://unpkg.com/leaflet/dist/leaflet.js"></script>  
<script>  
    var mymap = L.map('mapid').setView([35, 130], 1); // 设置地图视图中心点和缩放级别  
  
    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {  
        attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors',  
        maxZoom: 18,  
    }).addTo(mymap);  

    var ipCount = 50;
  
    function addLocationsToMap(locations) {  
        locations.forEach((location, index) => {  
            // 根据IP数量区间设置颜色类  
            let colorClass;  
            if (ipCount >= 0 && ipCount < 10) {  
                colorClass = 'green-triangle';  
            } else if (ipCount >= 10 && ipCount < 30) {  
                colorClass = 'blue-triangle';  
            } else {  
                colorClass = 'red-triangle';  
            }    
            // 解析Loc字符串为经纬度数组  
            var coords = location.Loc.split(',').map(Number);  
  
            // 创建一个SVG元素用于绘制红色三角形  
            var svgMarker = document.createElementNS("http://www.w3.org/2000/svg", "svg");  
            svgMarker.setAttribute("class", "marker");  
            svgMarker.setAttribute("width", "20");  
            svgMarker.setAttribute("height", "30");  
  
            var polygon = document.createElementNS("http://www.w3.org/2000/svg", "polygon");  
            polygon.setAttribute("class", colorClass);  
            polygon.setAttribute("points", "4,0 0,15 8,15"); // 三角形顶点坐标  
  
            svgMarker.appendChild(polygon);  
  
            // 使用L.DivIcon将SVG作为图标  
            var myIcon = L.divIcon({  
                className: 'my-custom-icon',  
                html: svgMarker.outerHTML,  
                iconSize: [20, 30], // 与SVG尺寸相匹配  
                iconAnchor: [10, 30], // 图标锚点  
                popupAnchor: [0, -30] // 弹出框锚点  
            });  
  
            // 将标记添加到地图上  
            L.marker(coords, {icon: myIcon}).addTo(mymap);  

            // 更新已处理的IP数量  
            ipCount--;  
  
            // 如果已经处理了50个，重置计数器  
            if (ipCount < 0) {  
                ipCount = 50;  
            } 
        });  
    }  
  
    // 使用fetch API从服务器获取数据  http://localhost:3000/location/get-latest
    fetch('https://personal-page-express-mongodb.onrender.com/api/locations/location/get-latest')  
        .then(response => response.json())  
        .then(data => {  
            // 假设返回的数据是一个数组  
            var locations = data.slice(0, 50);  
            addLocationsToMap(locations);  
        })  
        .catch(error => console.error('Error fetching data:', error));   
</script>  

<div class="like-button-container">
    <button id="like-button" onclick="incrementLike()">👍 Like</button>
    <span id="like-count">Loading...</span>
</div>

</body>

