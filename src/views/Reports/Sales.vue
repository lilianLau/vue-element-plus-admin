<script setup lang="tsx">
import { ContentWrap } from '@/components/ContentWrap'
import { useI18n } from '@/hooks/web/useI18n'
import { ref, reactive, unref } from 'vue'
import { Form, FormSchema } from '@/components/Form'
import { Table, TableColumn } from '@/components/Table'
import { getTreeTableListApi } from '@/api/table'
// import { ElTag } from 'element-plus'
import { useTable } from '@/hooks/web/useTable'
import { BaseButton } from '@/components/Button'
// import { useGuide } from '@/hooks/web/useGuide'

const { t } = useI18n()
// const { drive } = useGuide()

// Form schema
const treeSelectData = [
  { value: '1', label: 'FOOD' },
  { value: '2', label: 'NON-FOOD' },
  { value: '3', label: 'COLD CHAIN' }
]

const schema = ref<FormSchema[]>([
  {
    field: 'state',
    label: 'State',
    component: 'Select',
    componentProps: {
      options: [
        { label: 'SBH', value: 'sbh' },
        { label: 'KCH', value: 'kch' }
      ]
    }
  },
  {
    field: 'year',
    label: 'Year',
    component: 'DatePicker',
    componentProps: {
      type: 'year'
    }
  },
  {
    field: 'costCentre',
    label: 'Cost Centre',
    component: 'Select',
    componentProps: {
      options: [
        { label: 'SBH-BKI', value: 'sbhbki' },
        { label: 'SBH-BKI', value: 'sbhbki' }
      ]
    }
  },
  {
    field: 'date',
    label: 'Date',
    component: 'DatePicker',
    componentProps: {
      type: 'dates'
    }
  },
  {
    field: 'division',
    component: 'TreeSelect',
    label: 'Division',
    componentProps: {
      renderAfterExpand: false,
      multiple: true,
      showCheckbox: true,
      checkStrictly: true,
      checkOnClickNode: true,
      data: treeSelectData
    }
  },
  {
    field: 'week',
    label: 'Week',
    component: 'Select',
    componentProps: {
      options: [
        { label: 'W1', value: 'w1' },
        { label: 'W2', value: 'w2' }
      ]
    }
  },
  {
    field: 'subDivision',
    label: 'Sub Division',
    component: 'Select',
    componentProps: {
      options: [
        { label: 'FOOD 1 - 01', value: 'food1' },
        { label: 'FOOD 2 - 01', value: 'food2' }
      ]
    }
  },
  {
    field: 'binType',
    label: 'Bin Type',
    component: 'Select',
    componentProps: {
      options: [
        { label: 'GOOD BIN', value: 'goodbin' },
        { label: 'BAD BIN', value: 'badbin' }
      ]
    }
  },
  {
    field: 'subGroup',
    label: 'Sub Group',
    component: 'Select',
    componentProps: {
      options: [
        { label: 'INDOFOOD', value: 'indofood' },
        { label: 'PEP-QUAKER', value: 'pepquaker' }
      ]
    }
  },
  {
    field: 'locationName',
    label: 'Location Name',
    component: 'Select',
    componentProps: {
      options: [
        { label: 'BKI GEN WAREHOUSE LOCATION', value: 'bkigenwarehouselocation' },
        { label: 'BKI GEN WAREHOUSE LOCATION', value: 'bkigenwarehouselocation' }
      ]
    }
  },
  {
    field: 'stockCategoryName',
    label: 'Stock Category Name',
    component: 'Select',
    componentProps: {
      options: [
        { label: 'MOLFIX EXTRA DRY', value: 'molfixextradry' },
        { label: 'MOLFIX EXTRA DRY', value: 'molfixextradry' }
      ]
    }
  }
])

// const guideStart = () => {
//   drive()
// }

// Table setup
const { tableRegister, tableState } = useTable({
  fetchDataApi: async () => {
    const { currentPage, pageSize } = tableState
    const res = await getTreeTableListApi({
      pageIndex: unref(currentPage),
      pageSize: unref(pageSize)
    })
    return {
      list: res.data.list,
      total: res.data.total
    }
  }
})
const { loading, dataList, total, currentPage, pageSize } = tableState

const columns = reactive<TableColumn[]>([
  {
    field: 'selection',
    type: 'selection'
  },
  {
    field: 'index',
    label: t('tableDemo.index'),
    type: 'index'
  },
  {
    field: 'state',
    label: 'State',
    formatter: () => {
      return 'State Total'
    }
  },
  {
    field: 'seller_name',
    label: 'Seller Name',
    formatter: () => {
      return 'Seller Name'
    }
  },
  {
    field: 'content',
    label: 'NON FOOD GRAND TOTAL (Get from Food Category)',
    children: [
      {
        field: 'target',
        label: 'Target',
        formatter: () => {
          return '5,440.00'
        }
      },
      {
        field: 'sales',
        label: 'Sales',
        formatter: () => {
          return '4,360.00'
        }
      },
      {
        field: 'sales_achievement',
        label: 'Sales Achievement % (ACH)',
        formatter: () => {
          return '124.77%'
        }
      },
      {
        field: 'net_sales',
        label: 'Net Sales',
        formatter: () => {
          return '477.50'
        }
      },
      {
        field: 'bsr',
        label: 'BSR',
        formatter: () => {
          return '40.89'
        }
      },
      {
        field: 'bsr_vs_sales',
        label: 'BSR vs Sales',
        formatter: () => {
          return '0.94%'
        }
      },
      {
        field: 'reach',
        label: 'Reach %'
      },
      {
        field: 'mss',
        label: 'MSS %'
      }
    ]
  },
  {
    field: 'action',
    label: t('tableDemo.action'),
    slots: {
      default: (data) => {
        return (
          <BaseButton type="primary" onClick={() => actionFn(data)}>
            {t('tableDemo.action')}
          </BaseButton>
        )
      }
    }
  }
])

const actionFn = (data) => {
  console.log(data)
}
</script>

<template>
  <ContentWrap :title="t('guideDemo.guide')" :message="t('guideDemo.message')">
    <Form :schema="schema" label-width="150px" />
    <Table
      v-model:pageSize="pageSize"
      v-model:currentPage="currentPage"
      :columns="columns"
      :data="dataList"
      row-key="id"
      :loading="loading"
      sortable
      :pagination="{
        total: total
      }"
      @register="tableRegister"
    />
  </ContentWrap>
</template>

<style lang="less" scoped>
.el-button {
  margin-top: 10px;
}
</style>
