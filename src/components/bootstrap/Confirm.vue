<template>
  <div>
    <div class="modal-backdrop fade" :class="{in:isopen}"></div>
    <div class="modal fade" tabindex="-1" role="dialog" :class="{in:isopen}" style="display: block">
      <div class="modal-dialog" role="document" :class="{'modal-sm':bSize=='sm','modal-md':bSize=='md','modal-lg':bSize=='lg'}">
        <div class="modal-content">
          <div class="modal-header">
            <button type="button" class="close" data-dismiss="modal" aria-label="Close" @click="close"><span aria-hidden="true">&times;</span></button>
            <h4 class="modal-title">系统提示</h4>
          </div>
          <div class="modal-body">
            <div class="hbox">
              <div class="col" style="width: 35px"><i class="glyphicon  glyphicon-question-sign text-warning" style="font-size: 26px"></i></div>
              <div class="col">
                <div class=" text-sm m-t-xs">
                  <slot></slot>
                </div>
              </div>
            </div>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-default" @click="close">取消</button>
            <button type="button" class="btn btn-primary" @click="ok">确定</button>
          </div>
        </div>
        <!-- /.modal-content -->
      </div>
      <!-- /.modal-dialog -->
    </div>
    <!-- /.modal -->
  </div>
</template>
<script>
export default {
  data() {
    return {
      isopen: false
    }
  },
  props: ["bSize"],
  created: function() {
    var defclass = document.body.className;
    document.body.className = defclass + " modal-open";
    var _self = this;
    setTimeout(function() {
      _self.isopen = true;
    }, 1);
  },
  methods: {
    close: function() {
      var _self = this;
      _self.isopen = false;
      setTimeout(function() {
        _self.$emit('close');
        var defclass = document.body.className;
        document.body.className = defclass.replace(' modal-open', '');
      }, 160);
    },
    ok: function() {
      var _self = this;
      _self.isopen = false;
      setTimeout(function() {
        _self.$emit('ok');
        var defclass = document.body.className;
        document.body.className = defclass.replace(' modal-open', '');
      }, 160);
    }
  }
}

</script>
