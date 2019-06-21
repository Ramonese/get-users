<template>

<div class="card">
   <div class="card-header">
     <h2 class="mb-0">
      <button class="btn btn-link" type="button" data-toggle="collapse" v-bind:data-target="`#collapse-${user.id}`" v-bind:aria-controls="user.id">
          {{user.name}}
       </button>   
      </h2>
   </div>
    
    <div v-bind:id='`collapse-${user.id}`' class="collapse" >
      <div class="card-body">
       {{user.phone_number}}
       {{user.address}}
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


