<script setup>

   //defineProps(['title', 'text', ])

   const props = defineProps({
    title: String,
    id: Number,
    body: {
        type: String,
        default: 'Sin description'
    },
    fav: Function
   })

   const emit = defineEmits(['fav'])

  


</script>

<template>
    <div class="card">
        <div class="card-body">
            <h5 class="card-title">
                {{  id }} - {{ title }}
            </h5>
            <p> {{  body }}</p>
            <button @click="emit('fav', title)" class="btn btn-outline-primary"> Fav</button>
        </div>

    </div>

</template>