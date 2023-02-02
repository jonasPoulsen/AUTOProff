<template>
    <div class="create">
        <h1>Crteate page</h1>
        <CreateForm />
    </div>
</template>
  
<script>
import CreateForm from '@/components/CreateForm.vue'


export default {
    name: 'CreateView',
    components: {
        CreateForm,
    }
}
</script>
  