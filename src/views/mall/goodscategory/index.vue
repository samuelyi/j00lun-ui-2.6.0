<!--
  - Copyright (C) 2018-2019
  - All rights reserved, Designed By
  - 注意：
  - 本软件为 开发研制，未经购买不得使用
  - 购买后可获得全部源代码（禁止转卖、分享、上传到码云、github等开源平台）
  - 一经发现盗用、分享等行为，将追究法律责任，后果自负
-->
<template>
  <div class="execution">
    <basic-container>
      <avue-crud ref="crud"
                 :data="tableData"
                 :permission="permissionList"
                 :table-loading="tableLoading"
                 :option="tableOption"
                 :before-open="beforeOpen"
                 v-model="form"
                 @on-load="getPage"
                 @refresh-change="refreshChange"
                 @row-update="handleUpdate"
                 @row-save="handleSave"
                 @row-del="handleDel">
        <template slot="picUrlForm"
                  slot-scope="scope">
          <MaterialList v-model="scope.row.picUrl" type="image" :num=1 :width='scope.row.parentId == "0" ? 300 : 150' :height=150></MaterialList>
        </template>
        <template slot="picUrl" slot-scope="scope">
          <img
            style="height: 100px"
            :src="scope.row.picUrl">
        </template>
      </avue-crud>
    </basic-container>
  </div>
</template>

<script>
    import {getPage, fetchTree, getObj, addObj, putObj, delObj} from '@/api/mall/goodscategory'
    import {tableOption} from '@/const/crud/mall/goodscategory'
    import {mapGetters} from 'vuex'
    import MaterialList from '@/components/material/list.vue'

    export default {
        components: {
            MaterialList
        },
        name: 'goodscategory',
        data() {
            return {
                form: {},
                tableData: [],
                tableLoading: false,
                tableOption: tableOption,
                parentTreeData: []
            }
        },
        created() {
        },
        mounted: function () {
        },
        computed: {
            ...mapGetters(['permissions']),
            permissionList() {
                return {
                    addBtn: this.vaildData(this.permissions.mall_goodscategory_add, false),
                    delBtn: this.vaildData(this.permissions.mall_goodscategory_del, false),
                    editBtn: this.vaildData(this.permissions.mall_goodscategory_edit, false),
                    viewBtn: this.vaildData(this.permissions.mall_goodscategory_get, false)
                };
            }
        },
        methods: {
            beforeOpen(done,type){
                if(type == 'add'){
                  this.form.picUrl = []
                }
                if(type == 'edit'){
                  this.form.picUrl = [this.form.picUrl]
                }
                done()
            },
            getPage() {
                this.tableLoading = true
                fetchTree().then(response => {
                    let tableData = response.data.data
                    this.tableData = tableData
                    this.tableLoading = false
                }).catch(() => {
                    this.tableLoading = false
                })
            },
            /**
             * @title 数据删除
             * @param row 为当前的数据
             * @param index 为当前删除数据的行数
             *
             **/
            handleDel: function (row, index) {
                var _this = this
                this.$confirm('是否确认删除此数据', '提示', {
                    confirmButtonText: '确定',
                    cancelButtonText: '取消',
                    type: 'warning'
                }).then(function () {
                    return delObj(row.id)
                }).then(data => {
                    _this.$message({
                        showClose: true,
                        message: '删除成功',
                        type: 'success'
                    })
                    this.getPage()
                }).catch(function (err) {
                })
            },
            /**
             * @title 数据更新
             * @param row 为当前的数据
             * @param index 为当前更新数据的行数
             * @param done 为表单关闭函数
             *
             **/
            handleUpdate: function (row, index, done, loading) {
                row.picUrl = row.picUrl.length > 0 ? row.picUrl[0] : ''
                putObj(row).then(data => {
                    this.$message({
                        showClose: true,
                        message: '修改成功',
                        type: 'success'
                    })
                    done()
                    this.getPage()
                }).catch(() => {
                    loading()
                })
            },
            /**
             * @title 数据添加
             * @param row 为当前的数据
             * @param done 为表单关闭函数
             *
             **/
            handleSave: function (row, done, loading) {
                row.picUrl = row.picUrl.length > 0 ? row.picUrl[0] : ''
                addObj(row).then(data => {
                    this.$message({
                        showClose: true,
                        message: '添加成功',
                        type: 'success'
                    })
                    done()
                    this.getPage()
                }).catch(() => {
                    loading()
                })
            },
            /**
             * 刷新回调
             */
            refreshChange(val) {
              this.getPage(val.page)
            }
        }
    }
</script>

<style lang="scss" scoped>
</style>
