# mahas.js

#List

init
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
```
