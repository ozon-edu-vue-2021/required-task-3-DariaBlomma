<template>
  <div class="map">
    <h3>Карта офиса</h3>

    <div v-if="!isLoading" class="map-root">
      <!-- map -->
      <MapSvg ref="mapSvg" />
      <TableSvg v-show="false" ref="tableSvg" />
    </div>
    <div v-else>Loading...</div>
  </div>
</template>

<script>
import MapSvg from "@/assets/images/map.svg";
import TableSvg from "@/assets/images/workPlace.svg";
import * as d3 from "d3";
import legend from "@/assets/data/legend.json";
import tables from "@/assets/data/tables.json";

export default {
  components: {
    MapSvg,
    TableSvg,
  },
  data() {
    return {
      isLoading: false,
      svg: null,
      tableSvg: null,
      g: null,
      tables: [],
    };
  },
  mounted() {
    this.svg = d3.select(this.$refs.mapSvg);
    this.g = this.svg.select("g");
    this.tableSvg = d3.select(this.$refs.tableSvg);

    this.tables = tables;

    if (this.g) {
      this.drawTables();
    } else {
      console.log("ERROR");
    }
  },
  methods: {
    drawTables() {
      // создаем группу рабочих местм
      const svgTablesGroup = this.g.append("g").classed("groupPlaces", true);
      this.tables.forEach((table) => {
        // создать группу рабочего стола
        const svgTable = svgTablesGroup
          .append("g")
          .attr("transform", `translate(${table.x},${table.y}) scale(0.5)`)
          .attr("id", table._id)
          .classed("employer-place", true);

        svgTable
          .append("g")
          .attr("transform", `rotate(${table.rotate || 0})`)
          .attr("group_id", table.group_id)
          .html(this.tableSvg.html())
          .attr(
            "fill",
            legend.find((it) => it.group_id == table.group_id)?.color ??
              "transparent"
          );
      });
    },
  },
};
</script>

<style scoped>
.map {
  height: 100%;
  width: 100%;
  padding: 24px;
  overflow: hidden;
  box-sizing: border-box;
  display: flex;
  flex-direction: column;
}

.map-root {
  height: 100%;
  width: 100%;
  overflow: hidden;
  box-sizing: border-box;
}

h3 {
  margin-top: 0px;
}

::v-deep svg {
  height: 100%;
  width: 100%;
}

::v-deep .table {
  cursor: pointer;
}
</style>
