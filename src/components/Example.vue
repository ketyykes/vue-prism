<script setup>
import { onMounted } from "vue";
import Prism from "prismjs";
import "prismjs/components/prism-python";
import "prismjs/plugins/line-numbers/prism-line-numbers.js";
import "prismjs/plugins/line-numbers/prism-line-numbers.css";

onMounted(() => {
	window.Prism = window.Prism || {};
	window.Prism.manual = true;
	Prism.highlightAll();
});
</script>

<template>
	<div class="line-numbers">
		<pre><code class="language-python">
"""
created_at_utc  : 2024-09-19T12:45:10Z
created_at_w3c  : 2024-09-19T20:45:10+08:00
App_Version     : 3.1.0
Game_Session    : 12.5.4
game            : obstacle_avoid
game_version    : 2.0.1
"""

import pickle
import os
import sys
import io

sensor_data = None
predicted_speed = None
AI_model = None
left_wheel_speed = None
right_wheel_speed = None

if sys.stdout == sys.__stdout__:
    sys.stdout = io.TextIOWrapper(open(sys.stdout.fileno(), 'wb', 0), encoding='utf-8', write_through=True)


class GameAI:
    def __init__(self, ai_name, *args, **kwargs):
        global sensor_data, predicted_speed, AI_model, left_wheel_speed, right_wheel_speed
        sensor_data = []
        predicted_speed = []
        with open(os.path.join(os.path.dirname(__file__), 'ai_model' + '.pickle'), 'rb') as f:
            AI_model = pickle.load(f)
    def update(self, game_info, keyboard=[], *args, **kwargs):
        global sensor_data, predicted_speed, AI_model, left_wheel_speed, right_wheel_speed
        if game_info['status'] != "GAME_RUNNING":
            return "RESTART"
        else:
            # 收集感測器資料並進行速度預測
            sensor_data = [[game_info['L_sensor'], game_info['C_sensor'], game_info['R_sensor']]]
            predicted_speed = AI_model.predict(sensor_data).tolist()
            left_wheel_speed = predicted_speed[0][0]
            right_wheel_speed = predicted_speed[0][1]
            return {'left_speed': left_wheel_speed, 'right_speed': right_wheel_speed}
    def reset(self):
        global sensor_data, predicted_speed, AI_model, left_wheel_speed, right_wheel_speed
        print('遊戲已重置')
	</code></pre>
	</div>
</template>

<style scoped>
.read-the-docs {
	color: #888;
}
</style>
