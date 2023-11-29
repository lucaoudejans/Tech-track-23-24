<script>
    import { onMount } from 'svelte';
    import * as d3 from 'd3';
  
    let data = [
      { ancestry: 'pure blood', hairColor: 'blond', name: 'Draco Malfoy' },
      { ancestry: 'pure blood', hairColor: 'blond', name: 'Neville Longbottom' },
      { ancestry: 'halfblood', hairColor: 'black', name: 'Harry Potter' },
      { ancestry: 'pure blood', hairColor: 'black', name: 'Severus Snape' },
      { ancestry: 'pure blood', hairColor: 'red', name: 'Ron Weasley' },
      { ancestry: 'muggle', hairColor: 'brown', name: 'Hermione Granger' },
      { ancestry: 'pure blood', hairColor: 'brown', name: 'Sirius Black' },
    ];
  
    onMount(() => {
      // D3-code voor de dotplot
      const margin = { top: 20, right: 30, bottom: 30, left: 40 };
      const width = 400 - margin.left - margin.right;
      const height = 300 - margin.top - margin.bottom;
  
      const svg = d3
        .select('#dotplot-container')
        .append('svg')
        .attr('width', width + margin.left + margin.right)
        .attr('height', height + margin.top + margin.bottom)
        .append('g')
        .attr('transform', `translate(${margin.left},${margin.top})`);
  
      // Unieke waarden voor x-as en y-as
      const xValues = Array.from(new Set(data.map(d => d.ancestry)));
      const yValues = Array.from(new Set(data.map(d => d.hairColor)));
  
      const xScale = d3.scaleBand().domain(xValues).range([0, width]).padding(0.1);
      const yScale = d3.scaleBand().domain(yValues).range([height, 0]).padding(0.1);
  
      // Voeg x-as toe
      svg.append('g')
        .attr('transform', `translate(0,${height})`)
        .call(d3.axisBottom(xScale))
        .selectAll('.tick text')
        .attr('fill', 'black'); // Zet de kleur van de x-as labels op zwart
  
      // Voeg y-as toe
      svg.append('g')
        .call(d3.axisLeft(yScale))
        .selectAll('.tick text')
        .attr('fill', 'black'); // Zet de kleur van de y-as labels op zwart
  
      // Voeg cirkels toe aan de dotplot
      svg.selectAll('circle')
        .data(data)
        .enter()
        .append('circle')
        .attr('cx', d => xScale(d.ancestry) + xScale.bandwidth() / 2)
        .attr('cy', d => yScale(d.hairColor) + yScale.bandwidth() / 2)
        .attr('r', d => (d.ancestry === 'pure blood' && d.hairColor === 'blond') ? 8 : 5)
        .attr('fill', 'black'); // Zwart voor de dots
    });
  </script>
  
  <div id="dotplot-container"></div>
  