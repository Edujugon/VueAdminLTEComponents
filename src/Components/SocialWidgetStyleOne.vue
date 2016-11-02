<template>
    <div :class="'col-md-' + width">
        <!-- Widget: user widget style 1 -->
        <div class="box box-widget widget-user-2">
            <!-- Add the bg color to the header using any of the bg-* classes -->
            <div v-bind:class="{'text-center widget-user-header bg-yellow' : !image}">
                <div v-if="image" class="widget-user-image">
                    <img class="img-circle" src="image" alt="User Avatar">
                </div>
                <!-- /.widget-user-image -->
                <h3 v-bind:class="{ 'widget-user-username': image }">{{title}}</h3>
                <h5 v-bind:class="{ 'widget-user-desc': image }">{{subTitle}}</h5>
            </div>
            <div class="box-footer no-padding">
                <ul class="nav nav-stacked">
                    <li><a >{{totalLabel}} <span class="pull-right badge bg-blue">{{total}}</span></a></li>
                    <li><a >{{totalInvoicesLabel}} <span class="pull-right badge bg-blue">{{totalInvoices}}</span></a></li>
                    <li><a >{{dateStartLabel}} <span class="pull-right badge bg-aqua">{{dateStart}}</span></a></li>
                    <li><a >{{dateFinishLabel}} <span class="pull-right badge bg-aqua">{{dateFinish}}</span></a></li>
                </ul>
            </div>
        </div>
        <!-- /.widget-user -->
    </div>
</template>

<script>
    export default{
        props:{
            width:{
                default:4,
            },
            image:{},
            title:{},
            subTitle:{},
            totalLabel:{},
            totalInvoicesLabel:{},
            totalInvoices:{},
            total:{},
            dateStartLabel:{},
            dateFinishLabel:{},
            dateStart:{},
            dateFinish:{}
        },
        mounted(){
            console.log('Social Widget Style One Ready');
        }
    }
</script>