<script setup>
import OverView from '../components/AvailabilityPage/OverviewAvailability.vue'
import Return from '../components/AvailabilityPage/ReturnButton.vue'
import logo from '../components/DatePage/Logo.vue'
</script>

<template>
<body class="backG">
<ul><logo></logo></ul>
<h1 class="h1">Availability</h1>
<div class="availability">
<OverView></OverView>
<ul class="return">
<Return ></Return>
</ul>
</div>

</body>
</template>

<style scoped>

.backG{
        font-weight: normal;
  /* iphone 13 mini height and width*/
  height: 730px;
  width: 375px;
  position: relative;
       background: linear-gradient(180.02deg, #1B8E87 0.02%, #FFFFFF 92.97%);

}


.h1{
    padding: 10px;
  font-family: sans-serif;
  text-transform: uppercase;
  color: #fff;

  text-align: center;
  font-size: 2em;
  position: relative; top: 20px;
   text-shadow:
       3px 3px 0 #000,
     -1px -1px 0 #000,
      1px -1px 0 #000,
      -1px 1px 0 #000,
       1px 1px 0 #000;
}

.return{
  position: relative;
  bottom: -2cm;
  left: 1cm;
}




</style>