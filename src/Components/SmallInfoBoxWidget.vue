<template>
    <div :class="'col-md-' + width + 'col-sm-6 col-xs-12'">
        <div class="info-box">
            <span :class="'info-box-icon bg-' + color"><i :class="'fa' + icon"></i></span>

            <div class="info-box-content">
                <span class="info-box-text">{{heading}}</span>
                <span class="info-box-number">{{phrase}}</span>
            </div>
        </div>
    </div>
</template>

<script>
    export default{
        props: {
            width:{
                default:'3'
            },
            color:{
                default: 'aqua'
            },
            icon: {
                default: 'fa-star-o'
            },
            heading: {
                default: ''
            },
            phrase:{
                default: ''
            }
        },
        mounted() {
            console.log('SmallInfoBox Widget ready.')
        }
    }
</script>