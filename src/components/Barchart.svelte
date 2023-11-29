<script>
import { onMount } from 'svelte';
  import * as d3 from 'd3';

  let data = [
    {
      category: 'alive',
      value: 5,
      label: 'student',
      students: [
        'Harry Potter',
        'Hermione Granger',
        'Ron Weasley',
        'Neville Longbottom',
        'Draco Malfoy',
      ],
    },
    { category: 'deceased', value: 2, label: 'not a student' },
  ];

  onMount(async () => {

    // making a barchart
    const margin = { top: 20, right: 30, bottom: 30, left: 40 };
    const width = 400 - margin.left - margin.right;
    const height = 300 - margin.top - margin.bottom;

    const svg = d3
      .select('#chart-container')
      .append('svg')
      .attr('width', width + margin.left + margin.right + 100)
      .attr('height', height + margin.top + margin.bottom)
      .append('g')
      .attr('transform', `translate(${margin.left},${margin.top})`);

    const xScale = d3.scaleBand().domain(data.map((d) => d.category)).range([0, width]).padding(0.1);
    const yScale = d3.scaleLinear().domain([0, 7]).range([height, 0]);


// adding y line
    svg
      .append("line")
      .attr("x1", 0)
      .attr("x2", 0)
      .attr("y1", 0)
      .attr("y2", height)
      .attr("stroke", "black")
      .attr("stroke-width", 2);

// x line text
    svg
      .selectAll(".xlabel")
      .data(data)
      .enter()
      .append("text")
      .attr("class", "xlabel")
      .attr("x", (d) => xScale(d.category) + xScale.bandwidth() / 2)
      .attr("y", height + 25) // Afstand van de x-as lijn
      .attr("text-anchor", "middle")
      .text((d) => d.label);

// y line text
    svg
      .selectAll(".ylabel")
      .data(d3.range(1, 8)) // Array van 1 tot en met 7
      .enter()
      .append("text")
      .attr("class", "ylabel")
      .attr("x", -10) // Afstand van de y-as lijn
      .attr("y", (d) => yScale(d))
      .attr("text-anchor", "end")
      .attr("dy", 3) // Verplaatsing van de tekst
      .text((d) => d);

// adding the bars
    svg
        .selectAll(".bar")
        .data(data)
        .enter()
        .append("rect")
        .attr("class", (d) => d.category)
        .attr("x", (d) => xScale(d.category))
        .attr("y", (d) => yScale(d.value))
        .attr("width", xScale.bandwidth())
        .attr("height", (d) => height - yScale(d.value))
        .on("mouseover", handleMouseOver)
        .on("mouseout", handleMouseOut);

// adding x line (over bars)
    svg
      .append("line")
      .attr("x1", 0)
      .attr("x2", width)
      .attr("y1", height)
      .attr("y2", height)
      .attr("stroke", "black")
      .attr("stroke-width", 2);

// legend
    const legend = svg
      .append("g")
      .attr("transform", `translate(${width + 10}, 0)`); // Aan de rechterkant van de grafiek

    legend
      .append("rect")
      .attr("x", 0)
      .attr("y", 10)
      .attr("width", 20)
      .attr("height", 20)
      .attr("fill", "#5DBB63");

    legend
      .append("text")
      .attr("x", 30)
      .attr("y", 25)
      .text("Alive");

    legend
      .append("rect")
      .attr("x", 0)
      .attr("y", 40)
      .attr("width", 20)
      .attr("height", 20)
      .attr("fill", "#808080");

    legend
      .append("text")
      .attr("x", 30)
      .attr("y", 55)
      .text("Deceased");

// Colors of bars
    svg.selectAll(".alive").attr("fill", "#5DBB63");
    svg.selectAll(".deceased").attr("fill", "#808080");

// hover function
    function handleMouseOver(event, d) {
        const studentNames = d.students || [];

// To check if there's a tooltip
        let tooltip = d3.select('.tooltip');

        if (tooltip.empty()) {
// Add a tooltip if there's no tooltip
        tooltip = d3.select('body')
            .append('div')
            .attr('class', 'tooltip')
            .style('position', 'absolute')
            .style('color', 'black')
            .style('background-color', 'white')
            .style('border', '1px solid #ccc')
            .style('border-radius', '5px')
            .style('box-shadow', '0 2px 4px rgba(0, 0, 0, 0.1)')
            .style('display', 'block');
        }

    tooltip
      .html(`<strong>Students:</strong> ${getTooltipContent(d)}`)
      .style('left', event.pageX + 'px')
      .style('top', event.pageY + 'px');

    console.log('Student Names:', studentNames);
  }

  function handleMouseOut() {
// Let the tooltip disappear when you're not hovering anymore
    d3.select('.tooltip').remove();
  }

  function getTooltipContent(data) {
    if (data.category === 'deceased') {
      return 'Sirius Black<br>Severus Snape';
    } else {
      return data.students.join('<br>');
    }
  }
});
</script>

<main>
<div id="chart-container"></div>
</main>
