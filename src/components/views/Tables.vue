<template>
  <section class="content">
    <div class="row center-block">
      <h2>Data tables</h2>
      <div class="col-md-12">
        <div class="box">
          <div class="box-header">
            <h3 class="box-title">Powersupply data status</h3>
          </div>
          <!-- /.box-header -->
          <div class="box-body">
            <div class="dataTables_wrapper form-inline dt-bootstrap" id="example1_wrapper">
              <div class="row">
                <div class="col-sm-6">
                  <div id="example1_length" class="dataTables_length">

                  </div>
                </div>
              </div>
            <!-- <div>
              <button v-on:click="getdigit">I get data！</button>
            </div> -->
              <div class="row">
                <div class="col-sm-12 table-responsive">
                  <table aria-describedby="example1_info" role="grid" id="example1" class="table stripe table-bordered table-striped dataTable">
                  </table>
                </div>
              </div>
              <div class="row">
                <div class="col-sm-12 table-responsive">
                  <table aria-describedby="example1_info" role="grid" id="example2" class="table stripe table-bordered table-striped dataTable">
                  </table>
                </div>
              </div>
            </div>
            <!-- /.box-body -->
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import $ from 'jquery'
import api from '../../api'
// Require needed datatables modules
require('datatables.net')
require('datatables.net-bs')

export default {
  name: 'Tables',
  data () {
    return {
      data:[]
    }
  },
  methods :{
    getdigit(){
      api.request('get','/api/database').then(res=> {
         for (let index = 0; index < res.data.length; index++) {
           let list = new Array()  
           let value=JSON.stringify(res.data[index].value)
           let obdoc = JSON.parse(value)     
           list[0] = obdoc.Model;
           list[1] = obdoc.AssemblyPN;
           list[2] = obdoc.Cause;
           list[3] = obdoc.Year;
           list[4] = obdoc.Month;
           list[5] = obdoc.Qty; 
           list[6] = obdoc.VendorPN;
           list[7] = obdoc.ProdOrder;
           list[8] = obdoc.ExtSerialNo;
           list[9] = obdoc.IntSerialNo;
           list[10] = obdoc.DateCode;
           list[11] = obdoc.CompPN; 
           list[12] = obdoc.LotNo;
           list[13] = obdoc.CompSupplier;
           list[14] = obdoc.CompDesc;
           list[15] = obdoc.FailItem;
           list[16] = obdoc.FailDate;
          //  list[17] = "hello"
          //  list[17] = obdoc.Wk; 
           list[17] = obdoc.Manufacture;
           list[18] = obdoc.MainPart;
           list[19] = obdoc.CustomerPN;
           list[20] = obdoc.TestStation;
           list[21] = obdoc.DefectCodeDesc;
           list[22] = obdoc.DefectCode; 
           list[23] = obdoc.Category                     
           this.data[index]=list
         }
      }).then(()=>{
        $('#example1').DataTable( {
        "scrollY": '50vh',
        "scrollX": true,
        data: this.data,
        columns: [
              { title: 'Model' },
              { title: 'AssemblyPN' },
              { title: 'Cause' },
              { title: 'Year' },
              { title: 'Month' },
              { title: 'Qty' },
              { title: 'VendorPN' },
              { title: 'ProdOrder' },
              { title: 'ExtSerialNo' },
              { title: 'IntSerialNo' },
              { title: 'DateCode' },
              { title: 'CompPN' },
              { title: 'LotNo' }, 
              { title: 'CompSupplier' },
              { title: 'CompDesc' },
              { title: 'FailItem' },
              { title: 'FailDate' },
              { title: 'Manufacture' },
              { title: 'MainPart' },
              { title: 'CustomerPN' },
              { title: 'TestStation' },
              { title: 'DefectCodeDesc' },
              { title: 'DefectCode' },
              { title: 'Category' }
              // { title: 'WK' }  
        ]
    } )
       $('#example1').DataTable(
         {
        "scrollY": '50vh',
        "scrollX": true,
        data: this.data,
        columns: [
              { title: 'Model' },
              { title: 'AssemblyPN' },
              { title: 'Cause' },
              { title: 'Year' },
              { title: 'Month' },
              { title: 'Qty' },
              { title: 'VendorPN' },
              { title: 'ProdOrder' },
              { title: 'ExtSerialNo' },
              { title: 'IntSerialNo' },
              { title: 'DateCode' },
              { title: 'CompPN' },
              { title: 'LotNo' }, 
              { title: 'CompSupplier' },
              { title: 'CompDesc' },
              { title: 'FailItem' },
              { title: 'FailDate' },
              { title: 'Manufacture' },
              { title: 'MainPart' },
              { title: 'CustomerPN' },
              { title: 'TestStation' },
              { title: 'DefectCodeDesc' },
              { title: 'DefectCode' },
              { title: 'Category' }
              // { title: 'WK' }  
        ]
    }
       )
      }      
      )
    }
  },
  mounted() {
    this.getdigit()
  }
    // this.$nextTick(() => {
    //   $('#example1').DataTable()
    // })
}
</script>

<style>
/* Using the bootstrap style, but overriding the font to not draw in
   the Glyphicons Halflings font as an additional requirement for sorting icons.

   An alternative to the solution active below is to use the jquery style
   which uses images, but the color on the images does not match adminlte.

@import url('/static/js/plugins/datatables/jquery.dataTables.min.css');
*/

@import url('/static/js/plugins/datatables/dataTables.bootstrap.css');

table.dataTable thead .sorting:after,
table.dataTable thead .sorting_asc:after,
table.dataTable thead .sorting_desc:after {
  font-family: 'FontAwesome';
}

table.dataTable thead .sorting:after {
  content: '\f0dc';
}

table.dataTable thead .sorting_asc:after {
  content: '\f0dd';
}

table.dataTable thead .sorting_desc:after {
  content: '\f0de';
}
</style>
