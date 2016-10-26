<template>
    <div :class="'col-md-' + width + 'col-sm-6 col-xs-12'">
        <div :class="'info-box bg-' + color">
            <span class="info-box-icon"><i :class="'fa' + icon"></i></span>

            <div class="info-box-content">
                <span class="info-box-text">{{heading}}</span>
                <span class="info-box-number">{{phrase}}</span>

                <div class="progress">
                    <div class="progress-bar" :style="'width:' + percentage + '%'"></div>
                </div>
                <span class="progress-description">
                    {{description}}
                  </span>
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
                default: 'fa-bookmark-o'
            },
            heading: {
                default: ''
            },
            phrase:{
                default: ''
            },
            percentage: {
                default: '50'
            },
            description: {
                default: ''
            }
        },
        mounted() {
            console.log('MediumInfoBox Widget ready.')
        }
    }
</script>