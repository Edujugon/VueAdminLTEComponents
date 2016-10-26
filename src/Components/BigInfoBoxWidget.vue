<template>
    <div :class="'col-lg-' + width + ' col-xs-6'">
        <!-- small box -->
        <div :class="'small-box bg-' + color">
            <div class="inner">
                <h3>{{heading}}</h3>

                <p>{{phrase}}</p>
            </div>
            <div class="icon">
                <i :class="'fa ' + icon"></i>
            </div>
            <a v-if="url" :href="url" class="small-box-footer">{{moreInfo}} <i class="fa fa-arrow-circle-right"></i></a>
        </div>
    </div>
</template>
<script>
    export default {
        props:{
            width:{
                default:'3'
            },
            color:{
              default:'aqua'
            },
            heading:{
                default: ''
            },
            phrase:{
                default: ''
            },
            icon:{
                default: 'fa-star'
            },
            url: {
            },
            moreInfo:{
                default : 'More info'
            }
        },
        mounted() {
            console.log('BigInfoBox Widget ready.')
        }
    }
</script>