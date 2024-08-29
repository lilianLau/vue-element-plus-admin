<script setup lang="tsx">
import { ContentWrap } from '@/components/ContentWrap'
import { useI18n } from '@/hooks/web/useI18n'
import { ref, reactive, unref } from 'vue'
import { Form, FormSchema } from '@/components/Form'
import { Table, TableColumn } from '@/components/Table'
import { ElTabs, ElTabPane } from 'element-plus'
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
const { tableState } = useTable({
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
// const { loading, dataList, total } = tableState

// Hardcoded table data
const dataList = reactive([
  {
    id: '1',
    state: 'Total EM',
    seller_name: null,
    content: {
      target: '5440',
      sales: '4360',
      sales_achievement: '124.77%',
      net_sales: '477.5',
      bsr: '40.89',
      bsr_vs_sales: '0.94%'
    },
    children: []
  },
  {
    id: '2',
    state: 'Total SWK',
    seller_name: null,
    content: {
      target: '2520',
      sales: '2260',
      sales_achievement: '111.5%',
      net_sales: '345.8',
      bsr: '30.82',
      bsr_vs_sales: '1.36%'
    },
    children: []
  },
  {
    id: '3',
    state: 'Total KCH',
    seller_name: null,
    content: {
      target: '660',
      sales: '660',
      sales_achievement: '100%',
      net_sales: '105.1',
      bsr: '7.62',
      bsr_vs_sales: '1.15%'
    },
    children: [
      {
        id: '4',
        state: 'KCH KG01',
        seller_name: 'ABU',
        content: {
          target: '230',
          sales: '290',
          sales_achievement: '79.31%',
          net_sales: '65',
          bsr: '1.68',
          bsr_vs_sales: '0.58%'
        }
      },
      {
        id: '5',
        state: 'KCH KG02',
        seller_name: 'ALI',
        content: {
          target: '430',
          sales: '370',
          sales_achievement: '116.22%',
          net_sales: '40.1',
          bsr: '5.94',
          bsr_vs_sales: '1.61%'
        }
      }
    ]
  },
  {
    id: '6',
    state: 'TOTAL SBH',
    seller_name: null,
    content: {
      target: '2920',
      sales: '2100',
      sales_achievement: '139.05%',
      net_sales: '131.7',
      bsr: '10.07',
      bsr_vs_sales: '0.48%'
    },
    children: []
  },
  {
    id: '7',
    state: 'Total KK',
    seller_name: null,
    content: {
      target: '860',
      sales: '580',
      sales_achievement: '148.28%',
      net_sales: '37.9',
      bsr: '4.21',
      bsr_vs_sales: '0.73%'
    },
    children: [
      {
        id: '8',
        state: 'KK-AG01',
        seller_name: 'AHMAD',
        content: {
          target: '930',
          sales: '710',
          sales_achievement: '130.99%',
          net_sales: '34.1',
          bsr: '3.73',
          bsr_vs_sales: '0.53%'
        }
      },
      {
        id: '9',
        state: 'KK-AG02',
        seller_name: 'ADULAH',
        content: {
          target: '1130',
          sales: '810',
          sales_achievement: '139.51%',
          net_sales: '59.7',
          bsr: '2.13',
          bsr_vs_sales: '0.26%'
        }
      }
    ]
  }
])

const columns = reactive<TableColumn[]>([
  {
    field: 'selection',
    type: 'selection'
  },
  {
    field: 'index',
    label: 'No.',
    type: 'index'
  },
  {
    field: 'state',
    label: 'State',
    width: '150px'
  },
  {
    field: 'seller_name',
    label: 'Seller Name',
    width: '150px'
  },
  {
    field: 'content',
    label: 'NON FOOD GRAND TOTAL (Get from Food Category)',
    children: [
      {
        field: 'target',
        label: 'Target',
        width: '100px',
        formatter: (row) => row.content.target
      },
      {
        field: 'sales',
        label: 'Sales',
        width: '100px',
        formatter: (row) => row.content.sales
      },
      {
        field: 'sales_achievement',
        label: 'Sales Achievement % (ACH)',
        width: '230px',
        formatter: (row) => row.content.sales_achievement
      },
      {
        field: 'net_sales',
        label: 'Net Sales',
        formatter: (row) => row.content.net_sales
      },
      {
        field: 'bsr',
        label: 'BSR',
        formatter: (row) => row.content.bsr
      },
      {
        field: 'bsr_vs_sales',
        label: 'BSR vs Sales',
        formatter: (row) => row.content.bsr_vs_sales
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

// Tabs setup
const activeTab = ref('first') // Default active tab
</script>

<template>
  <ContentWrap :title="t('guideDemo.guide')" :message="t('guideDemo.message')">
    <!-- Tabs Section -->
    <ElTabs v-model="activeTab">
      <ElTabPane label="Format 6" name="first">
        <!-- Content for Tab 1-->
        <Form :schema="schema" label-width="150px" label-position="left" />
        <Table :columns="columns" :data="dataList" row-key="id" sortable />
        <div style="padding-right: 10px; margin-top: 10px; text-align: right">
          Total: {{ dataList.length }}
        </div>
      </ElTabPane>
      <ElTabPane label="Sample Tab" name="second">
        <!-- Content for Tab 2 -->
        <p>This is content for Tab 2.</p>
      </ElTabPane>
    </ElTabs>
  </ContentWrap>
</template>

<style lang="less" scoped>
.el-button {
  margin-top: 10px;
}
</style>
