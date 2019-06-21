<template>

<div class="card border-0">
   <!-- <div class="card-header bg-white border"> -->
     <a class="card-header bg-white border" data-toggle="collapse" v-bind:data-target="`#collapse-${user.id}`" v-bind:aria-controls="user.id">
  <div class="row justify-content-between">
          <span class="col col-sm-auto"><h2 class="h6">{{user.name}}</h2></span>
          <span class="col col-sm-auto "><small class="text-muted">{{user.phone_number}}</small></span> 
        </div>  
      </a>
   <!-- </div> -->
    <div v-bind:id='`collapse-${user.id}`' class="collapse bg-light" >
      <div class="card-body">
        <ul>
          <li><strong>Name:</strong> {{user.name}}</li>
          
          <li><strong>Address:</strong> {{user.address}}</li>
          <li v-if="user.email"><strong>Email:</strong> {{user.email}}</li>
        </ul>  
      </div>
    </div>

</div> 

</template>

<script>
export default {
  name: 'Users',
  props: ['user'] 
}
</script>


