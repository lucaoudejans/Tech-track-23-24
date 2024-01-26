<script>
// importing onmount and d3
  import { onMount } from 'svelte';
  import * as d3 from 'd3';

// array with data that will be used
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

  onMount(() => {

// Making a barchart
    const margin = { top: 20, right: 30, bottom: 30, left: 40 };
    const width = 400 - margin.left - margin.right;
    const height = 300 - margin.top - margin.bottom;

// group element to svg + how big
    const svg = d3
      .select('#chart-container')
      .append('svg')
      .attr('width', width + margin.left + margin.right + 100)
      .attr('height', height + margin.top + margin.bottom)
      .append('g')
      .attr('transform', `translate(${margin.left},${margin.top})`);

// Unique values for x and y lines
    const xScale = d3.scaleBand().domain(data.map((d) => d.category)).range([0, width]).padding(0.1);
    const yScale = d3.scaleLinear().domain([0, 7]).range([height, 0]);


// Adding y line
    svg
      .append("line")
      .attr("x1", 0)
      .attr("x2", 0)
      .attr("y1", 0)
      .attr("y2", height)
      .attr("stroke", "black")
      .attr("stroke-width", 2);

// Text for x line
    svg
      .selectAll(".xlabel")
      .data(data)
      .enter()
      .append("text")
      .attr("class", "xlabel")
      .attr("x", (d) => xScale(d.category) + xScale.bandwidth() / 2)
      .attr("y", height + 25) 
      .attr("text-anchor", "middle")
      .text((d) => d.label);

// Text for y line
    svg
      .selectAll(".ylabel")
      .data(d3.range(1, 8))
      .enter()
      .append("text")
      .attr("class", "ylabel")
      .attr("x", -10)
      .attr("y", (d) => yScale(d))
      .attr("text-anchor", "end")
      .attr("dy", 3)
      .text((d) => d);


      const tooltip = d3.select('#tooltip');
// Adding the bars
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
        .style("cursor", "pointer")
        // tooltip fixes, roept functie met data aan met mouse over
        .on("mouseover", function (event, d) {
          tooltip
          .transition()
          .duration(200)
          .style('opacity', 1);
          tooltip
            .html(`${getTooltipContent(d)}`)
            .style('display', 'block')
            .style('left', event.pageX + 'px')
            .style('top', event.pageY + 'px');
        })
        .on("mouseout", function () {
            tooltip
            .transition()
            .duration(200)
            .style('opacity', 0)
            .style('display', 'none');
        });

// Adding x line (over bars)
    svg
      .append("line")
      .attr("x1", 0)
      .attr("x2", width)
      .attr("y1", height)
      .attr("y2", height)
      .attr("stroke", "black")
      .attr("stroke-width", 2);

// Legend
    const legend = svg
      .append("g")
      // put it right to the visualisation
      .attr("transform", `translate(${width + 10}, 0)`);

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

// hover for second bar
  function getTooltipContent(data) {
    if (data.category === 'deceased') {
      return 'Sirius Black<br>Severus Snape';
    } else {
      return data.students.join('<br>');
    }
  }
});
</script>
<div id="tooltip" class="tooltip"> </div>
<div id="chart-container"></div>

