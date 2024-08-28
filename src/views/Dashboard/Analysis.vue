<script setup lang="tsx">
import { ContentWrap } from '@/components/ContentWrap'
import { useI18n } from '@/hooks/web/useI18n'
import { Table, TableColumn } from '@/components/Table'
import { getTableListApi } from '@/api/table'
import { TableData } from '@/api/table/types'
import { ref } from 'vue'
// import { ref, h } from 'vue'
// import { ElTag } from 'element-plus'
// import { BaseButton } from '@/components/Button'

interface Params {
  pageIndex?: number
  pageSize?: number
}

const { t } = useI18n()

const columns: TableColumn[] = [
  {
    field: 'index',
    label: t('tableDemo.no'),
    type: 'index'
  },
  {
    field: 'pageviews',
    label: t('tableDemo.state')
  },
  {
    field: 'pageviews',
    label: t('tableDemo.branch')
  },
  {
    field: 'title',
    label: t('tableDemo.costcentrecode')
  },
  {
    field: 'pageviews',
    label: t('tableDemo.area')
  },
  {
    field: 'title',
    label: t('tableDemo.description')
  },
  {
    field: 'pageviews',
    label: t('tableDemo.month')
  },
  {
    field: '-',
    label: '-'
  },
  {
    field: 'display_time',
    label: t('tableDemo.documentDate'),
    sortable: true
  },
  {
    field: 'author',
    label: 'Doc Type'
  },
  {
    field: '-',
    label: 'Project'
  },
  {
    field: 'pageviews',
    label: 'Doc#'
  },
  {
    field: '-',
    label: 'Our Do No'
  },
  {
    field: '-',
    label: 'Delivery Term'
  },
  {
    field: 'pageviews',
    label: 'Debtor Area Code'
  },
  {
    field: 'author',
    label: 'Debtor Area Name'
  },
  {
    field: 'pageviews',
    label: 'Debtor Category Code'
  },
  {
    field: 'author',
    label: 'Debtor Category Name'
  },
  {
    field: 'author',
    label: 'Category Type'
  },
  {
    field: 'author',
    label: 'Doc Sales Person Code'
  },
  {
    field: 'author',
    label: 'Doc Sales Person Name'
  },
  {
    field: 'pageviews',
    label: 'Customer Code'
  },
  {
    field: 'author',
    label: 'Customer Name'
  },
  {
    field: 'author',
    label: 'Stock Location Code'
  },
  {
    field: 'author',
    label: 'Stock Location Name'
  },
  {
    field: 'author',
    label: 'Bin Type'
  },
  {
    field: 'author',
    label: 'Stock Group Name'
  },
  {
    field: 'author',
    label: 'Stock Group Code'
  },
  {
    field: '-',
    label: 'SubGroup'
  },
  {
    field: 'author',
    label: 'Stock Category Code'
  },
  {
    field: 'author',
    label: 'Stock Category Name'
  },
  {
    field: 'author',
    label: 'Stock Class Code'
  },
  {
    field: 'author',
    label: 'Stock Class Name'
  },
  {
    field: 'author',
    label: 'Remark1'
  },
  {
    field: 'author',
    label: 'Remark2'
  },
  {
    field: 'author',
    label: 'Remark3'
  },
  {
    field: 'author',
    label: 'Remark4'
  },
  {
    field: 'author',
    label: 'Remark5'
  },
  {
    field: '-',
    label: 'Division'
  },
  {
    field: '-',
    label: 'SubDivision'
  },
  {
    field: 'author',
    label: 'Stock Code'
  },
  {
    field: 'author',
    label: 'Barcode'
  },
  {
    field: 'author',
    label: 'Stock Name'
  },
  {
    field: 'author',
    label: 'Stock Name2'
  },
  {
    field: 'index',
    label: 'Sales Qty'
  },
  {
    field: 'author',
    label: 'BASED QTY UOM'
  },
  {
    field: 'pageviews',
    label: 'RATE'
  },
  {
    field: 'pageviews',
    label: 'CTN QTY'
  },
  {
    field: 'pageviews',
    label: 'Currency'
  },
  {
    field: '-',
    label: 'Item Unit Price'
  },
  {
    field: '-',
    label: 'Gross Price'
  },
  {
    field: '-',
    label: 'Disc'
  },
  {
    field: '-',
    label: 'Disc Amnt'
  },
  {
    field: '-',
    label: 'Discount 1'
  },
  {
    field: '-',
    label: 'Discount 1 Amount'
  },
  {
    field: '-',
    label: 'Discount 2'
  },
  {
    field: '-',
    label: 'Discount 2 Amount'
  },
  {
    field: '-',
    label: 'Discount 3'
  },
  {
    field: '-',
    label: 'Discount 3 Amount'
  },
  {
    field: '-',
    label: 'Tax Code'
  },
  {
    field: '-',
    label: 'Tax'
  },
  {
    field: '-',
    label: 'Sales Value'
  },
  {
    field: '-',
    label: 'Reference No'
  },
  {
    field: '-',
    label: 'Reference 1'
  },
  {
    field: '-',
    label: 'Reference 2'
  },
  {
    field: '-',
    label: 'Reference 3'
  },
  {
    field: '-',
    label: 'Reference 4'
  },
  {
    field: '-',
    label: 'Reference 5'
  },
  {
    field: '-',
    label: 'Remark 1'
  },
  {
    field: '-',
    label: 'Remark 2'
  },
  {
    field: '-',
    label: 'Remark 3'
  },
  {
    field: '-',
    label: 'Remark 4'
  },
  {
    field: '-',
    label: 'Remark 5'
  },
  {
    field: '-',
    label: 'Reason Code'
  },
  {
    field: '-',
    label: 'Reason'
  },
  {
    field: '-',
    label: 'Transfer From'
  },
  {
    field: '-',
    label: 'Transfer To'
  },
  {
    field: '-',
    label: 'Transfer To AIN Date'
  }
]

const loading = ref(true)

const tableDataList = ref<TableData[]>([])

const getTableList = async (params?: Params) => {
  const res = await getTableListApi(
    params || {
      pageIndex: 1,
      pageSize: 10
    }
  )
    .catch(() => {})
    .finally(() => {
      loading.value = false
    })
  if (res) {
    tableDataList.value = res.data.list
  }
}

getTableList()

// const actionFn = (data: any) => {
//   console.log(data)
// }
</script>

<template>
  <ContentWrap :title="t('router.rawData')">
    <Table
      :columns="columns"
      :data="tableDataList"
      :loading="loading"
      :defaultSort="{ prop: 'display_time', order: 'descending' }"
      class="raw-data-table"
    />
  </ContentWrap>
</template>
<style>
.raw-data-table .el-table__header .cell {
  padding: 0 4px;
  overflow: visible;
  white-space: wrap;
  overflow-wrap: normal;
}
</style>
