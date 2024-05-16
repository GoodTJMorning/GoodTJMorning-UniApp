<template>
    <view>
		<uni-nav-bar
		  @clickLeft="goBack"
		  left-icon="back"
		  leftIcon="arrowleft"
		  title="楼长订单"
		  statusBar="true"
		  fixed="true"
		  color="#ffffff"
		  backgroundColor="#a7f3c9"
		></uni-nav-bar>
        <view class="tabs">
            <view class="tab" :class="{ active: activeTab === 0 }" @tap="activeTab = 0">待派送</view>
            <view class="tab" :class="{ active: activeTab === 1 }" @tap="activeTab = 1">已完成</view>
        </view>
        <!-- <view v-if="activeTab === 0">
			<uni-search-bar @confirm="handleSearch" v-model="searchKeyword"></uni-search-bar>
			<uni-table :columns="columnsDelivery" :list="orderListDelivery"></uni-table>
			<text>{{ JSON.stringify(orderListDelivery) }}</text>
			
		</view>
		<view v-if="activeTab === 1">
			<uni-search-bar @confirm="handleSearch" v-model="searchKeyword"></uni-search-bar>
			<uni-table :columns="columnsFinished" :list="orderListFinished"></uni-table>
			<text>{{ JSON.stringify(orderListFinished) }}</text>
		</view> -->
		

		<div v-if="activeTab === 0">
		  <!-- <p>待派送订单</p> -->
		  <view class="box_order_lists" v-for="order in orderListDelivery" :key="order.orderId">
		  <table>
			<tbody>
			  <tr>
				<td>订单号：{{ order.orderId }}</td>
				<td>顾客名：{{ order.customerName }}</td>
				<td>手机号：{{ order.phoneNumber }}</td>
				<td>派送地址：{{ order.address }}</td>
				<td><button @click="finished(order.orderId)">派送完成</button></td>
			  </tr>
			</tbody>
		
		  </table>
		  </view>
		</div>
		<div v-if="activeTab === 1">
		  <!-- <p>已完成订单</p> -->
		  <view class="box_order_lists" v-for="order in orderListFinished" :key="order.orderId">
		  <table>
			<tbody>
				<td>订单号：{{ order.orderId }}</td>
				<td>手机号：{{ order.phoneNumber }}</td>
				<td>订单状态：{{ order.status }}</td>
			</tbody>
		  </table>
		  </view>
		</div>

    </view>
</template>

<script>
import { employeeLogin } from "../api/api";
export default {

    data() {
        return {
            activeTab: 0,
            searchKeyword: '',
            columnsDelivery: [
                { label: '订单号', prop: 'orderId', width: '200' },
                { label: '手机号', prop: 'phoneNumber', width: '200' },
                { label: '操作', prop: 'operation', width: '200', type: 'button', operation: [
                { name: '派送完成', event: 'finished' },
                ]}
            ],
            columnsFinished: [
                { label: '订单号', prop: 'orderId', width: '200' },
                { label: '手机号', prop: 'phoneNumber', width: '200' },
                { label: '状态', prop: 'status', width: '200' },
            ],
            orderListDelivery: [
                { orderId: '123', phoneNumber: '1234567890' , address: '友圆8号楼', customerName: '胡先生'},
                { orderId: '789', phoneNumber: '1122334455' , address: '友圆19号楼', customerName:'李女士'},
				
            ],
            orderListFinished: [
                { orderId: '456', phoneNumber: '0987654321', status: '已完成' },
                { orderId: '321', phoneNumber: '6655443322', status: '已完成' },
            ],
        }
    },
    methods: {
        handleTabClick(e) {
            this.activeTab = e.index;
        },
        handleSearch(keyword) {
            this.searchKeyword = keyword;
            this.filterData();
        },
        filterData() {
            // 根据this.searchKeyword过滤数据
        },
		goBack() {
		  uni.redirectTo({
		    url: "/pages/my/my",
		  });
		}
		
    }
}
</script>
<style scoped>
.tabs {
	display: flex;
	justify-content: space-between;
}
.tab {
	flex: 1;
	text-align: center;
	padding: 10px 0;
	color: #999;
}
.tab.active {
	color: #333;
	border-bottom: 2px solid #333;
}
.box_order_lists{
	border-radius: 20px;
	background-color: #ffffff;
	margin: 10px;
}
table {
	width: 100%;
	border-collapse: collapse;
	margin-bottom: 30px;
}
th, td {
	padding: 10px;
	text-align: left;
}
th {
	background-color: #f5f5f5;
	font-weight: bold;
}
tr:nth-child(even) {
	background-color: #f2f2f2;
}
button {
	background-color: #148F77;
	color: white;
	border: none;
	border-radius: 10px;
	padding: 5px 10px;
}
button:hover {
	background-color: #45B39D;
	cursor: pointer;
}
</style>