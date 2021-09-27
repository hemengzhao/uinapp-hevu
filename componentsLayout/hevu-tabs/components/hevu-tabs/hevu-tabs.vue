<template>
	<view class="hevu-tabs" :style="{backgroundColor: backColor}">
		<scroll-view scroll-x="true">
			<view :class="`hevu-tabs-con ${type == 'back' ? 'con_back' : ''}`" ref='hevu-tabs-con' >
				<view :class="`back tabs${k} ${_index == k ? 'active' : ''}`" :ref='`tabs${k}`' 
				v-for='(item, k) in list' :key='k' :style="{borderColor: activeColor}"
				@click.stop="onClick(item, k)">
					<text :style="{color: activeColor}" v-if='_index == k'>{{item.name || item}}</text>
					<text v-else>{{item.name || item}}</text>
				</view>
			</view>
			<view :class="`border ${animated ? 'animated' : ''}`" :style="{width: borderWidth + 'px', left: borderLeft + 'px'}"></view>
		</scroll-view>
	</view>
</template>

<script>
	/**
	 * type{String} tabs类型  line   back
	 * list{Array}  tabs数据了列表  数据格式['张三'， '里斯'] 或者 [{name: '张三'}， {name: '里斯'}]  //neme显示
	 * backColor{String}  tabs背景颜色
	 * activeColor{String}  选中高亮颜色
	 * activeKey{String}  选中高亮key值依据  默认空置以索引为准
	 * activeValue{Number | String} 初时选中id或索引
	 * animated{boolean}  下划线动画
	 * 
	 * */
	export default {
		name: 'HevuTabs',
		props: {
			type: {
			  type: String,
			  default: 'line'
			},
			list: {
				type: Array,
				default () {
					return []
				}
			},
			activeColor: {
				type: String,
				default: '#007aff'
			},
			backColor: {
				type: String,
				default: '#fff'
			},
			activeKey: {
				type: String,
				default: ''
			},
			activeValue: {
				type: Number | String,
				default: 0,
			},
			animated: { //是否展示下划线滑动效果
				type: Boolean,
				default: true,
			}
			
		},
		data(){
			return {
				active: -1,
				borderLeft: 0,
				borderWidth: 0,
				justifyContent: 'space-around' //
			}
		},
		computed: {
			_index: function(){
				if(this.active > -1){
					return this.active;
				}
				if(this.activeKey){
					return this.list.findIndex(val => val[this.activeKey] == this.activeValue);
				}
				return this.activeValue;
				
			}
		},
		watch: {
			list: function(){
				this.countActiveFn();
			}
		},
		mounted() {
			this.countActiveFn();
		},
		methods:{
			onClick(item, k){
				// 计算下划线位置,长度
				const info = this.$refs[`tabs${k}`][0].$el.getBoundingClientRect();
				this.borderLeft = this.$refs[`tabs${k}`][0].$el.offsetLeft;
				this.borderWidth = info.width;
				this.active = k;
				this.$emit('click', item, k);
			},
			countActiveFn(){
				this.$nextTick(() => {
					// 判断justifyContent值
					const endinfo = this.$refs[`tabs${this.list.length - 1}`][0]?.$el?.offsetLeft;
					const bodyinfo = this.$refs[`hevu-tabs-con`][0]?.$el?.getBoundingClientRect() || {};
					if(endinfo > bodyinfo.width){
						this.justifyContent = 'flex-start' ;
					}
					
					// 计算下划线位置
					const info = this.$refs[`tabs${this._index}`][0]?.$el?.getBoundingClientRect() || {};
					this.borderLeft = this.$refs[`tabs${this._index}`][0]?.$el?.offsetLeft || 0;
					this.borderWidth = info.width || 0;
				})
			},
			scroll(){
				
			}
		}
	}
</script>

<style lang="scss" scoped>
	.hevu-tabs{
		width: 100%;
		position: relative;
		overflow: auto;
		.border{
			position: absolute;
			bottom: 0;
			height: 2px;
			border-radius: 1px;
			background-color: #007aff;
			&.animated{
				transition: all .3s;
			}
		}
		&-con{
			min-width: 100%;
			display: flex;
			white-space: nowrap;
			.back{
				line-height: 80rpx;
				padding: 0 20rpx;
				flex: 1;
				text-align: center;
				display: inline-block;
				border-radius: 10rpx;
				margin: 0 1px;
			}
			&.con_back{
				.back.active{
					margin: 0;
					border: 1px solid red;
					border-bottom: 0px;
				}
			}
		}
		
		
	}
</style>
