<template>
	<div>
		<h4>{{name}}</h4>
		<h5>上级:{{fname}} 下级:{{sname}} 同级:{{tname}}</h5>
		<button @click="bt">{{name}}触发{{fname}} </button>
		<button @click="tbtb">{{name}}触发{{tname}} </button>
		<sun :fname="fname" :zname="name" @stz="stz" @sname="snamez"></sun>
	</div>
</template>

<script>
	import sun from "@/components/sun"
	import {bus} from "@/bus.js"

	export default {
		name: 'App',
		props: ['fname'],
		components: {
			sun
		},
		data() {
			return {
				name: "子组件B",
				sname:"",
				tname:""
			}
		},
		methods: {
			bt(){
				this.$emit("ztf")
			},
			stz(){
				alert("我是"+this.name+"事件")
			},
			zname(){
				this.$emit('zname', this.name)
			},
			snamez(data){
				this.sname = data
			},
			tbtb(){
				bus.$emit("tbtb")
			}
		},
		mounted(){
			this.$emit("znameb", this.name);
			this.$emit("sname", this.sname);

			bus.$emit("tnameb",this.name)
		},
		created(){
			bus.$on("tnamea", data => (this.tname = data));
			bus.$on('tbta' ,function(){
	            this.stz()
	        }.bind(this));
		}
	}
</script>

<style scoped="">
	div{
		background: #F56C6C;
	}
</style>