<template>
	<picker-address-select
	  v-show="false"
	  v-model="address"
	  @on-get-addressIds="getAddressIds"
	  @on-get-addressNames="getAddressNames"></picker-address-select>
</template>

<script>
import PickerAddressSelect from '../../AppPicker/PickerAddressSelect'
export default {
	data() {
		return {
			address: []
		}
	},
	methods: {
		getCurrentPosition: function() {
			if(window.plus) {
				plus.geolocation.getCurrentPosition((position) => {
					let address = position.address;
					let addressNames = [address.province,address.city,address.district];
					this.address = addressNames;
				},(error) => {
					
				},{
					timeout: 10000,
					provider: 'amap'
				})
			}
			else {
				console.log('请使用hbuilder打包后获取当前位置');
			}
		},
		getAddressIds: function(ids) {
			this.$emit('on-get-localtionIds',ids);
		},
		getAddressNames: function(names) {
			this.$emit('on-get-localtionNames',names);
		}
	},
	created() {
		this.getCurrentPosition();
	},
	components: {
		PickerAddressSelect
	}
}
</script>