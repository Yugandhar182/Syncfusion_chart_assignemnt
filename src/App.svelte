<script>
   
    import Metric from "./metric.svelte";
    import Time from './time.svelte';
    import Placement from "./placement.svelte"
	import Rejected from "./rejectedreasons.svelte";
  

</script>

<div class="main-container">
    <Metric />
    <Time/>
    <Placement/>
    <div class="container2">
       <Rejected/>
    </div>
</div>

<style>
    .main-container {
        background-color:rgb(219, 214, 243);
        width: 1500px;
        height: 1500px;
        margin-left:10px;
        margin-top:-79px;
    }

    .container2 {
        width: 1400px;
        height: 420px;
   
        margin-top: 70px;
        margin-left:40px;
        background-color: white;
    }
 
  
</style>
