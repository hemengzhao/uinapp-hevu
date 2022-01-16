<template>
	<view class="hevu-text-sliding-vode" @click="makeCode">
		<canvas canvas-id="s-canvas" :style="{width: contentWidth + 'px', height: contentHeight + 'px'}"></canvas>
	</view>
</template>

<script>
	/**
	 * @param {Boolean} isInsideCode 验证码是否内部更新生成
	 * @param {Number} codeLength 验证码长度 最小值位2 最大值位8（isInsideCode位true有效）
	 * @param {Boolean} isCodetypeNumber 验证码是否位纯数字（isInsideCode位true有效）
	 * @param {Boolean} isCodeCasesensitive 验证码是否区分大小写（isInsideCode位true有效）
	 * @param {Function} verification 验证方法  参数code 返回布尔值（isInsideCode位true有效）
	 * 
	 * @param {String} identifyCode 需要展示的验证码
	 * @param {Number} fontSizeMin 字体大小 最小值
	 * @param {Number} fontSizeMax 字体大小 最大值
	 *  @param {string} backgroundColor 背景颜色色值最小值 最小值为0   
	 * @param {Number} backgroundColorMin 背景颜色色值最小值 最小值为0   
	 * @param {Number} backgroundColorMax 背景颜色色值最大值 最大值为255 
	 * @param {Number} colorMin 字体颜色色值最小值 最大值为0
	 * @param {Number} colorMax 字体颜色色值最大值 最大值为255 
	 * @param {Number} lineColorMin 干扰线颜色色值最小值 最小值为0
	 * @param {Number} lineColorMax 干扰线颜色色值最大值 最大值为255 
	 * @param {Number} dotColorMin 干扰点颜色色值最小值 最小值为0
	 * @param {Number} dotColorMax 干扰点颜色色值最大值 最大值为255 
	 * @param {Boolean} isDot 是否需要干扰点  
	 * @param {Boolean} isLine 是否需要干扰线
	 * @param {Number} contentWidth 画布宽度  
	 * @param {Number} contentWidth 画布宽度  
	 * @param {Number} contentHeight 画布高度 
	 *
	 * 
	 * */  
	export default {
		name: 'HevuTextSlidingVode',
		data(){
			return {
				code: '',
			}
		},
		props: {
			isInsideCode: {
				type: Boolean,
				default: false,
			},
			codeLength: {
				type: Number,
				default: 4,
			},
			isCodetypeNumber: {
				type: Boolean,
				default: false,
			},
			isCodeCasesensitive: {
				type: Boolean,
				default: true,
			},
			
			identifyCode: {
			  type: String,
			  default: "1234"
			},
			fontSizeMin: {
			  type: Number,
			  default: 35
			},
			fontSizeMax: {
			  type: Number,
			  default: 35
			},
			backgroundColor: {
				type: String,
				default: ''
			},
			backgroundColorMin: {
			  type: Number,
			  default: 180
			},
			backgroundColorMax: {
			  type: Number,
			  default: 240
			},
			colorMin: {
			  type: Number,
			  default: 50
			},
			colorMax: {
			  type: Number,
			  default: 160
			},
			lineColorMin: {
			  type: Number,
			  default: 100
			},
			lineColorMax: {
			  type: Number,
			  default: 200
			},
			dotColorMin: {
			  type: Number,
			  default: 0
			},
			dotColorMax: {
			  type: Number,
			  default: 255
			},
			isDot: {
			  type: Boolean,
			  default: true
			},
			isLine: {
			  type: Boolean,
			  default: true
			},
			contentWidth: {
			  type: Number,
			  default: 120
			},
			contentHeight: {
			  type: Number,
			  default: 40
			}
		},
		components: {

		},
		watch: {
			identifyCode: {
				handler: function(e){
					if(!this.isInsideCode){
						this.code = e;
						this.drawPic()
					}
				}
			}
		},
		mounted() {
			this.viewRefresh()
		},
		methods: {
			// 生成一个随机数
			randomNum(min, max){
				return Math.floor(Math.random() * (max - min) + min);
			},
			// 生成一个随机的颜色
			randomColor(min, max){
				let r = this.randomNum(min, max);
				let g = this.randomNum(min, max);
				let b = this.randomNum(min, max);
				return "rgb(" + r + "," + g + "," + b + ")";
			},
			transparent(){
				return "rgb(255,255,255)";
			},
			drawPic(){
				
				let ctx = uni.createCanvasContext("s-canvas");
				ctx.textBaseline = "bottom";
				// 绘制背景
				if(this.backgroundColor){
					ctx.setFillStyle(this.backgroundColor)
				} else {
					ctx.fillStyle = this.randomColor(
						this.backgroundColorMin,
						this.backgroundColorMax
					);
				}
				ctx.fillRect(0, 0, this.contentWidth, this.contentHeight);
				// 绘制文字
				for (let i = 0; i < this.code.length; i++) {
					this.drawText(ctx, this.code[i], i);
				}
				// 绘制背景
				this.isLine && this.drawLine(ctx)
				this.isDot && this.drawDot(ctx)
				ctx.draw()
			},
			drawText(ctx, txt, i){
				ctx.fillStyle = this.randomColor(this.colorMin, this.colorMax);
				ctx.font = this.randomNum(this.fontSizeMin, this.fontSizeMax) + "px SimHei";
				let x = (i + 1) * (this.contentWidth / (this.code.length + 1));
				let y = this.randomNum(this.fontSizeMax, this.contentHeight - 5);
				var deg = this.randomNum(-10, 10);
				// 修改坐标原点和旋转角度
				ctx.translate(x, y);
				ctx.rotate((deg * Math.PI) / 180);
				ctx.fillText(txt, 0, 0);
				// 恢复坐标原点和旋转角度
				ctx.rotate((-deg * Math.PI) / 180);
				ctx.translate(-x, -y);
			},
			drawLine(ctx){
				// 绘制干扰线
				for (let i = 0; i < 8; i++) {
				ctx.strokeStyle = this.randomColor(
				  this.lineColorMin,
				  this.lineColorMax
				);
				ctx.beginPath();
				ctx.moveTo(
				  this.randomNum(0, this.contentWidth),
				 this.randomNum(0, this.contentHeight)
				);
				ctx.lineTo(
				  this.randomNum(0, this.contentWidth),
				  this.randomNum(0, this.contentHeight)
				);
				ctx.stroke();
				}
			},
			drawDot(ctx){
				// 绘制干扰点
				for (let i = 0; i < 100; i++) {
					ctx.fillStyle = this.randomColor(0, 255);
					ctx.beginPath();
					ctx.arc(
					  this.randomNum(0, this.contentWidth),
					  this.randomNum(0, this.contentHeight),
					  1,
					  0,
					  2 * Math.PI
					);
					ctx.fill();
				}
			},
			randomText(){
				if(this.isCodetypeNumber){
					const arr = [0,1,2,3,4,5,6,7,8,9]
					return arr[Math.floor((Math.random()*10))]
				}
				const arr = ["A","B","C","D","E","F","G","H","I","J","K","L","M","N","O","P","Q","R","S","T","U","V","W","X","Y","Z",
				                "a","b","c","d","e","f","g","h","i","j","k","l","m","n","o","p","q","r","s","t","u","v","w","x","y","z",
				                0,1,2,3,4,5,6,7,8,9]
				                return arr[Math.floor((Math.random()*62))];
			},
			makeCode(){
				if(this.isInsideCode){
					this.code = '';
					const lenght = this.codeLength <= 0 || this.codeLength > 8 ? 4 : this.codeLength
					for (let i = 0; i < this.codeLength; i++) {
						this.code += this.randomText()
					}
					this.drawPic()
				}
			},
			verification(code){
				if(this.isInsideCode){
					let type;
					if(!this.isCodeCasesensitive){
						// toLowerCase 把字符串转换为小写。
						// toUpperCase 把字符串转换为大写
						type = code.toLowerCase() == this.code.toLowerCase();
					} else {
						type = code == this.code;
					}
					
					return type;
				}
				
			},
			// 视图重载
			viewRefresh(){
				if(!this.isInsideCode){
					
					this.code = this.identifyCode;
					this.drawPic()
				} else {
					this.makeCode()
				}
			}
			
		}
	}
</script>

<style lang="scss" scoped>
	.hevu-text-sliding-vode{
		display: inline-block;
	}
</style>
