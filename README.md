#include<stdio.h>

int main() {
	int leixing; //伤害类型
	double basic_attack, a1, a2, a3, a4; //基础，信赖，模组，潜能，技能
	double rate, rate1, rate2, rate3; //攻击速度，攻速加成（模组，天赋，技能）
	double t; //技能持续时间/弹药数量
	double beilv = 1, dps, dph; //伤害乘算倍率，dps,dph
	int judge; //技能类型判断
	double zongshang;
	int cishu;

	printf("注意：\n1.所有非整数变量都以小数形式输入，不要输入百分数\n2.若某项数据不存在，则输入0\n");
	printf("请问该技能伤害类型为？（若是物理输入0，是法术则输入1）");
	scanf("%d", &leixing);

	printf("该技能是弹药类技能吗？（若是输入1，不是则输入0）");
	scanf("%d", &judge);

	switch (judge) {
	case 0:
		printf("依次输入该干员的基础攻击，信赖加攻，模组加攻，潜能加攻，该技能的攻击加算数值\n");
		scanf("%lf %lf %lf %lf %lf", &basic_attack, &a1, &a2, &a3, &a4);

		printf("依次输入该干员的基础攻击速度，模组加攻速，天赋加攻速，技能加攻速\n");
		scanf("%lf %lf %lf %lf", &rate, &rate1, &rate2, &rate3);

		printf("输入技能的攻击乘算加成数值\n");
		scanf("%lf", &beilv);
		beilv = beilv ? beilv : 1; // 若乘算倍率为0则默认设置为1

		printf("输入技能持续时间\n");
		scanf("%lf", &t);

		double interval = 100.0 / (rate + rate1 + rate2 + rate3);
		cishu = (interval > 0) ? (int)(t / interval) : 0;

		dph = ((basic_attack + a1 + a2 + a3) * (1 + a4)) * beilv;
		zongshang = dph * cishu;
		dps = zongshang / t;
		break;

	case 1:
		printf("依次输入该干员的基础攻击，信赖加攻，模组加攻，潜能加攻，该技能的攻击加算数值\n");
		scanf("%lf %lf %lf %lf %lf", &basic_attack, &a1, &a2, &a3, &a4);

		printf("依次输入该干员的基础攻击速度，模组加攻速，天赋加攻速，技能加攻速\n");
		scanf("%lf %lf %lf %lf", &rate, &rate1, &rate2, &rate3);

		printf("输入技能的攻击乘算加成数值\n");
		scanf("%lf", &beilv);
		beilv = beilv ? beilv : 1; // 若乘算倍率为0则默认设置为1

		printf("输入弹药数量\n");
		scanf("%lf", &t);

		dph = ((basic_attack + a1 + a2 + a3) * (1 + a4)) * beilv;
		zongshang = dph * t;
		dps = dph / (100.0 / (rate + rate1 + rate2 + rate3));
		break;

	default:
		printf("别胡闹，不然就放血狗破军出来咬你\n");
		return 1;
	}

	printf("总伤：%.2f, dps：%.2f, dph：%.2f\n", zongshang, dps, dph);
	return 0;
}

