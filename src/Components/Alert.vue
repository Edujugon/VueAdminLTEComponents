<template>
    <div :class="'alert alert-' + type + ' alert-dismissible'">
        <button v-if="canBeClosed" type="button" class="close" data-dismiss="alert" aria-hidden="true">&times;</button>
        <h4><i :class="'icon fa fa-' + icon"></i> {{title}}</h4>
        {{message}}
    </div>
</template>

<script>
    export default{
        props:{
            type:{
                default: 'danger' // danger, info, warning, success
            },
            title:{
                default:'Alert!'
            },
            message:{

            },
            icon:{
                default:'ban' //ban, info , warning, check
            },
            canBeClosed:{
                default:true
            }
        },
        mounted() {
            console.log('Alert ready.');
        }
    }
</script>