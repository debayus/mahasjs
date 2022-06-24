# mahas.js

# List

html
```
<!-- tag id -->
<div class="card" id="table_Sample">

    <div class="card-header header-elements-inline">
        <h5 class="card-title">Sample</h5>
        <div class="header-elements">
            <div class="list-icons">
                <!-- open modal form -->
                <a class="list-icons-item" data-action="plus" href="javascript:isetup_Sample.openModal('POST')"></a>
                <!-- refresh table -->
                <a class="list-icons-item" data-action="reload" href="javascript:itable_Sample.refresh()"></a>
            </div>
        </div>
    </div>
    
    <!-- form table to refresh -->
    <form class="itable-form card-body">
        <input type="hidden" class="itable-pagesize" value="20" />
        <div class="row">
          <div class="col-md-3">
          
             <!-- filter -->
            <div class="form-group">
              <label for="Filter">Filter</label>
              <input type="text" id="Filter" data-itable-filter="Filter" placeholder="Filter" class="form-control" value="" />
            </div>
            
          </div>
        </div>
        <input type="submit" class="d-none"/>
    </form>
    
    <!-- table -->
    <div class="datatable-scroll">
        <table class="table table-hover dataTable table-xs table-striped">
            <thead>
                <tr class="bg-slate">
                    <th class="sorting text-left" data-itable-sorting="0">Name</th>
					<th class="text-center" style="width: 30px;">Action</th>
                </tr>
            </thead>
            <tbody></tbody>
        </table>
    </div>
</div>
```

init js
```
var itable_Sample = new iTable({
  id: 'table_Sample', // tag id
  url: '/api/list', // url to get data
  urlType:{
      DELETE : '/api/data' // url delete data
  },
  orderBy: 0, // default order by index
  orderByType: true, // default true for ascending, false for ascending 
  success: (r, t) => {
      if (r.success) {
          let tbody = '';
          if (r.datas.length === 0) tbody += t.trempty();
          $.each(r.datas, (i, v) => {
              tbody += '<tr>';

              // JS Columns
              tbody += `<td class="text-left">${v.name}</td>`;
              // ----- JS Columns

              tbody += '<td class="text-center">';
              tbody += '<div class="list-icons">';
              tbody += '<div class="dropdown">';
              tbody += '<a href="#" class="list-icons-item" data-toggle="dropdown"><i class="icon-menu9"></i></a>';
              tbody += '<div class="dropdown-menu dropdown-menu-right">';

              // JS Action
              tbody += `<a class="dropdown-item" href="javascript:isetup_Sample.openModal('GET',{ Id : '${v.id}' })"><i class="icon-eye"></i> Details</a></li>`;
              tbody += `<a class="dropdown-item" href="javascript:isetup_Sample.openModal('PUT',{ Id : '${v.id}' })"><i class="icon-pencil"></i> Edit</a></li>`;
              tbody += `<a class="dropdown-item" href="javascript:itable_Sample.delete({ Id : '${v.id}' }, itable_Sample)"><i class="icon-trash"></i> Delete</a></li>`;
              // ----- JS Columns

              tbody += '</div>';
              tbody += '</div>';
              tbody += '</div>';
              tbody += '</td>';
              tbody += '</tr>';
          });
          $(t.id).find('tbody').html(tbody);
          t.generateTableFooter(r.totalCount, r.pageSize, r.pageIndex);
      }
  }
  });
  
  // refresh table
  itable_Sample.refresh();
```
