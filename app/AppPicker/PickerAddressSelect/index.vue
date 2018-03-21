<template>
	<group :gutter="marginTop">
		<x-address
		  v-model="addressSelcted"
		  title="所在地区"
		  placeholder="请选择"
		  :hide-district="hideDistrict"
		  :readonly="readonly"
		  :list="addressList"
		  @on-hide="hide"
		  @on-shadow-change="changeValue"></x-address>
	</group>
</template>

<script>
import { Group, XAddress, ChinaAddressV4Data } from 'vux'
export default {
	props: {
		value: {
			type: Array,
			required: true,
			default() {
				return [];
			}
		},
		marginTop: {
			type: String,
			default() {
				return '-1px';
			}
		},
		readonly: {
			type: Boolean,
			default() {
				return false;
			}
		},
		hideDistrict: {
			type: Boolean,
			default() {
				return false
			}
		}
	},
	data() {
		return {
			addressSelcted: this.value,
			addressList: ChinaAddressV4Data,
			localAddressIDs: [],
			localAddressNames: []
		}
	},
	watch: {
		value: {
			handler: function(newArray) {
				this.addressSelcted = newArray;
			},
			deep: true
		}
	},
	methods: {
		changeValue: function(ids,names) {
			this.localAddressIDs = ids;
			this.localAddressNames = names;
			if(this.addressSelcted.length > 0) {
				this.$emit('on-get-addressIds', ids);
				this.$emit('on-get-addressNames', names);
			}
		},
		hide: function(confirm) {
			if(confirm) {
				this.$emit('on-confirm-addressIds',this.localAddressIDs);
				this.$emit('on-confirm-addressNames',this.localAddressNames);
			}
		}
	},
	components: {
		Group, XAddress
	}
}
</script>