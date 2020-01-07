<template>
    <div class="home">
        <div class="inner"></div>
        <div id="myChart"></div>
    </div>
</template>

<script lang="ts">
export default {
    name: 'Home',
    data() {
        return {
            home: {},
            player: {},
            active: {},
            user: {},
            login: {},
            info: {},
            history: {},
            collect: {},
            about: {},
        }
    },
    created() {
        let that = this;
        that.onData();
    },
    mounted() {
        let that = this;
    },
    methods: {
        onData: function() {
            let that = this;
            that.$axios.post('/api/report/compute', {}, {})
            .then(function(res){
                console.log(res, '/api/report/compute');
                if (res.data.status) {
                    that.home['home_show1'] = res.data['home_show1'];
                    that.home['home_click'] = res.data['home_click'];
                    that.player['player_show1']  = res.data['player_show1'];
                    that.player['player_show2']  = res.data['player_show2'];
                    that.active['active_show1']  = res.data['active_show1'];
                    that.user['user_show1']     = res.data['user_show1'];
                    that.user['user_click1']    = res.data['user_click1'];
                    that.user['user_click2']    = res.data['user_click2'];
                    that.user['user_click3']    = res.data['user_click3'];
                    that.user['user_click4']    = res.data['user_click4'];
                    that.user['user_click5']    = res.data['user_click5'];
                    that.login['login_show1']   = res.data['login_show1'];
                    that.login['login_click1']   = res.data['login_click1'];
                    that.info['info_show1']    = res.data['info_show1'];
                    that.history['history_show1'] = res.data['history_show1'];
                    that.history['history_click1'] = res.data['history_click1'];
                    that.history['history_click2'] = res.data['history_click2'];
                    that.collect['collect_show1'] = res.data['collect_show1'];
                    that.collect['collect_click1'] = res.data['collect_click1'];
                    that.collect['collect_click2'] = res.data['collect_click2'];
                    that.collect['collect_click3'] = res.data['collect_click3'];
                    that.about['about_show1'] = res.data['about_show1'];

                    that.onTable();
                } else {
                    that.$toast(that, 'error', '数据错误～');
                }
            })
			.catch(function(err) {
				that.$toast(that, 'error', '网络错误～');
			})
        },
        onTable: function() {
            let that = this;
            console.log(that.home['home_click'], '3333')
            let myChart = that.$echarts.init(document.getElementById('myChart'))
            myChart.setOption({
                title: {
                    text: '活跃度折线图'
                },
                tooltip: {
                    trigger: 'axis'
                },
                legend: {
                    data: []
                },
                grid: {
                    left: '3%',
                    right: '4%',
                    bottom: '3%',
                    containLabel: true
                },
                toolbox: {
                    feature: {
                        saveAsImage: {}
                    }
                },
                xAxis: {
                    type: 'category',
                    boundaryGap: false,
                    data: [
                        '1:00', '2:00', '3:00', '4:00', '5:00', '6:00', '7:00','8:00', '9:00', '10:00', '11:00', '12:00',
                        '13:00', '14:00', '15:00', '16:00', '17:00', '18:00', '19:00','20:00', '21:00', '22:00', '23:00', '24:00'
                    ]
                },
                yAxis: {
                    type: 'value'
                },
                series: [
                    {
                        name: 'Home页面-视频列表',
                        type: 'line',
                        stack: '总量',
                        data: that.home['home_show1']
                    },
                    {
                        name: 'Home页面-资源点击',
                        type: 'line',
                        stack: '总量',
                        data: that.home['home_click']
                    },
                    {
                        name: 'Player视频-视频播放',
                        type: 'line',
                        stack: '总量',
                        data: that.player['player_show1']
                    },
                    {
                        name: 'Player视频-显示广告',
                        type: 'line',
                        stack: '总量',
                        data: that.player['player_show2']
                    },
                    {
                        name: 'Active活动-活动页展示',
                        type: 'line',
                        stack: '总量',
                        data: that.active['active_show1']
                    },
                    {
                        name: 'User我的-我的显示',
                        type: 'line',
                        stack: '总量',
                        data: that.user['user_show1']
                    },
                    {
                        name: 'User我的-登录',
                        type: 'line',
                        stack: '总量',
                        data: that.user['user_click1']
                    },
                    {
                        name: 'User我的-用户信息',
                        type: 'line',
                        stack: '总量',
                        data: that.user['user_click2']
                    },
                    {
                        name: 'User我的-历史记录',
                        type: 'line',
                        stack: '总量',
                        data: that.user['user_click3']
                    },
                    {
                        name: 'User我的-收藏',
                        type: 'line',
                        stack: '总量',
                        data: that.user['user_click4']
                    },
                    {
                        name: 'User我的-关于我们',
                        type: 'line',
                        stack: '总量',
                        data: that.user['user_click5']
                    },
                    {
                        name: 'Login登录-登录页展示',
                        type: 'line',
                        stack: '总量',
                        data: that.login['login_show1']
                    },
                    {
                        name: 'Login登录-点击注册',
                        type: 'line',
                        stack: '总量',
                        data: that.login['login_click1']
                    },
                    {
                        name: 'Info用户信息-用户信息展示',
                        type: 'line',
                        stack: '总量',
                        data: that.info['info_show1']
                    },
                    {
                        name: 'History历史-显示历史记录',
                        type: 'line',
                        stack: '总量',
                        data: that.history['history_show1']
                    },
                    {
                        name: 'History历史-显示历史记录',
                        type: 'line',
                        stack: '总量',
                        data: that.history['history_click1']
                    },
                    {
                        name: 'History历史-显示历史记录',
                        type: 'line',
                        stack: '总量',
                        data: that.history['history_click2']
                    },
                    {
                        name: 'Collect收藏-显示收藏页',
                        type: 'line',
                        stack: '总量',
                        data: that.collect['collect_show1']
                    },
                    {
                        name: 'Collect收藏-视频播放',
                        type: 'line',
                        stack: '总量',
                        data: that.collect['collect_click1']
                    },
                    {
                        name: 'Collect收藏-跳登录',
                        type: 'line',
                        stack: '总量',
                        data: that.collect['collect_click2']
                    },
                    {
                        name: 'Collect收藏-取消收藏',
                        type: 'line',
                        stack: '总量',
                        data: that.collect['collect_click3']
                    },

                    {
                        name: 'About关于我们-显示关于我们',
                        type: 'line',
                        stack: '总量',
                        data: that.about['about_show1']
                    }
                ]
            });
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="less">
.home {
    width: 100%;
    height: 100%;
    background-color: #ffffff;
}
.inner {
    width: 100%;
    height: 300px;
}
#myChart {
    margin: 0 auto;
    width: 92%;
    height: 380px;
}
</style>