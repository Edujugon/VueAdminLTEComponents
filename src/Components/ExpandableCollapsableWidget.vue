<template>
    <div class="col-md-3">
        <div class="box box-default" v-bind:class="{'collapsed-box': !collapse}">
            <div class="box-header with-border">
                <h3 class="box-title">{{heading}}</h3>

                <div class="box-tools pull-right">
                    <button type="button" class="btn btn-box-tool" data-widget="collapse"><i class="fa fa-plus"></i>
                    </button>
                </div>
                <!-- /.box-tools -->
            </div>
            <!-- /.box-header -->
            <div class="box-body">
                {{body}}
            </div>
            <!-- /.box-body -->
        </div>
        <!-- /.box -->
    </div>

</template>
<script>
    export default{
        props:{
            heading:{},
            body:{},
            collapse:{
                default:false
            }
        }
    }
</script>