---
title: World map
layout: page
---

Behold; the map of the known world!

<svg version="1.1"
     baseProfile="full"
     id="worldmap"
     xmlns="http://www.w3.org/2000/svg"
     xmlns:xlink="http://www.w3.org/1999/xlink">
  <style type="text/css">
  circle, rect, polygon {
    visibility: hidden;
  }

  circle:target, rect:target, polygon:target {
    visibility: visible;
  }

  .area {
    stroke-dasharray: 5,5;
    stroke-width: 3;
    fill: transparent;
  }

  .path {
    visibility: visible;
    stroke-dasharray: 2,2;
    stroke-width: 3;
    stroke: magenta;
    fill: transparent;
  }
  </style>
  <image x="0" y="0" id="worldmapimage" xlink:href="{{ site.data.map.map_location }}" />
  {% assign color_definitions = site.data.map.colors %}
  {% for area in site.data.map.areas %}
    {% if area[1].color.size > 0 %}
      {% assign color = area[1].color %}
    {% else %}
      {% assign color = "defaultcolor" %}
    {% endif %}
    {% for _color in color_definitions %}
      {% if color == _color[0] %}
        {% assign color = _color[1] %}
        {% break %}
      {% endif %}
    {% endfor %}

    {% assign is_odd = area[1].coords.size | modulo: 2 %}

    {% if area[1].coords.size == 2 %}
    <circle cx="{{ area[1].coords[0] }}" 
            cy="{{ area[1].coords[1] }}" 
            r="5" 
            id="{{ area[0] }}"
            fill="{{ color }}" />
    {% elsif area[1].coords.size == 3 %}
    <circle cx="{{ area[1].coords[0] }}" 
            cy="{{ area[1].coords[1] }}" 
            r="{{ area[1].coords[2] }}" 
            id="{{ area[0] }}"
            class="area"
            style="stroke: {{ color }};"/>
    {% elsif area[1].coords.size == 4 %}
    <rect x="{{ area[1].coords[0] }}"
          y="{{ area[1].coords[1] }}"
          width="{{ area[1].coords[2] | minus: area[1].coords[0] }}"
          height="{{ area[1].coords[3] | minus: area[1].coords[1] }}"
          id="{{ area[0] }}"
          class="area"
          style="stroke: {{ color }};"/>
    {% elsif area[1].coords.size == 0 %}
    {% elsif area[1].coords.size == 1 %}
    {% elsif is_odd == 1 %}
    {% else %}
    <polygon points="{{ area[1].coords | join }}"
             id="{{ area[0] }}"
             class="area"
             style="stroke: {{ color }};"/>
    {% endif %}
  {% endfor %}

  {% for path in site.data.map.paths %}
    <polyline points="{{ path[1].coords | join }}"
              id="{{ path[0] }}"
              class="path" />
  {% endfor %}
</svg>

<script>
//<![CDATA[
var mapImage = document.getElementById("worldmapimage");
var theMap = document.getElementById("worldmap");
var imgObj = new Image();
imgObj.onload = function() {
  mapImage.setAttribute("height", imgObj.height);
  mapImage.setAttribute("width", imgObj.width);
  theMap.setAttribute("viewBox", "0 0 " + imgObj.width + " " + imgObj.height);
}
imgObj.src = mapImage.getAttributeNS("http://www.w3.org/1999/xlink", "href");

if (window.location.hash.match(/^#p?\d+(,\d+)*,?$/)) {
  var points = window.location.hash.replace(/,/g, ' ');
  points = points.substring(1);

  if (points[0] == 'p') {
    points = points.substring(1);
    points = points.split(" ");
    var command = "M " + points[0] + " " + points[1];
    for (var i = 2; i < points.length; ) {
      command += " L " + points[i++] + " " + points[i++];
    }
    var path = document.createElementNS("http://www.w3.org/2000/svg", "polyline");
    //path.setAttribute("d", command);
    path.setAttribute("points", points);
    /*
    path.style.visibility = "visible";
    path.style.stroke = "{{ site.data.map.colors.defaultcolor }}";
    path.style.strokeWidth = "3";
    path.style.strokeDasharray = "5,5";
    path.style.fill = "transparent";
    */
    path.classList.add("path");
    theMap.appendChild(path);
  }
  else {
    var area = document.createElementNS("http://www.w3.org/2000/svg", "polygon");
    area.style.visibility = "visible";
    area.style.fill = "{{ site.data.map.colors.defaultcolor }}";
    area.setAttribute("points", points);
    theMap.appendChild(area);
  }
}
//]]>
</script>
