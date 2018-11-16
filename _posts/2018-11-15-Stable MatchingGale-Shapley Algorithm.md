---
layout: post
title: Stable Matching:Gale-Shapley Algorithm
categories: Notes
description: 1962年，美国数学家David Gale和Lloyd Shapley发明了一种寻找稳定婚姻的策略，人们称之为延迟认可算法（Gale-Shapley算法）
keywords: 
---

#### Problem

​	假设有N个男女，每个人都对异性有一个喜欢程度的排名，怎么样为这群单身男女牵线搭桥能让最后匹配的婚姻都是稳定的？

​	当然是让每个人都和自己心目中的“梦中情人”在一起是最佳，但是现实往往没有那么美好。例如，A的第一选择是B，但是B的第一选择是C，那么A和B就不可能同时满足。所以婚姻中稳定才是解决问题的关键：A和B、C和D最后在一起，但是在A心目中C较B是最好的选择，而刚刚好的是C心中A较D也是最佳选择，则没人能阻止AC的情投意合，因此需要一个巧妙的方法来解决这个问题。

#### Solution

​	1962年，美国数学家David Gale和Lloyd Shapley发明了一种寻找稳定婚姻的策略，人们称之为延迟认可算法（Gale-Shapley算法）。

​	算法采用男生主动出击追女生的形式。

​	当还存在单身男生时，完成下述步骤：

​	1）每一位单身男性都选择自己心目中排名第一位的女生，并向她表白：

​	①被表白的女生没有被追求过，那么暂时答应这位男生。

​	②这位女生已被表白，她将正在追求她的单身男生与其当前男友进行比较，选择其中排名优先的男士作为其男友，即若更喜欢现在表白的单身男性，则抛弃前男友；否则保留其男友，拒绝别人。

​	2）经过1）中的步骤后有些男生已经有了女朋友，有些人依旧单身。在第二轮中，所有单身的男性将拒绝自己的女性从心仪列表中删除，在那些没拒绝自己的女孩中选出最中意的那个表白。这个女生无论是否被表白过，都可由1）中算法解决。持续下去，直到无人单身。

#### Algorithm

~~~python
import collections

#The women that the men prefer
preferred_rankings_men = {
	'ryan': 	['lizzy', 'sarah', 'zoey', 'daniella'],
	'josh': 	['sarah', 'lizzy', 'daniella', 'zoey'],
	'blake': 	['sarah', 'daniella', 'zoey', 'lizzy'],
	'connor': 	['lizzy', 'sarah', 'zoey', 'daniella']
}

#The men that the women prefer
preferred_rankings_women = {
	'lizzy': 	['ryan', 'blake', 'josh', 'connor'],
	'sarah': 	['ryan', 'blake', 'connor', 'josh'],
	'zoey':  	['connor', 'josh', 'ryan', 'blake'],
	'daniella':	['ryan', 'josh', 'connor', 'blake'] 
}

#Keep track of the people that "may" end up together
tentative_engagements 	= []

#Men who still need to propose and get accepted successfully
free_men 				= []

def init_free_men():
	'''Initialize the arrays of women and men to represent 
		that they're all initially free and not engaged'''
	# for man in preferred_rankings_men.iterkeys():
	for man in list(preferred_rankings_men):
		free_men.append(man)

def begin_matching(man):
	'''Find the first free woman available to a man at
		any given time'''

	print("DEALING WITH %s"%(man))
	for woman in preferred_rankings_men[man]:

		#Boolean for whether woman is taken or not
		taken_match = [couple for couple in tentative_engagements if woman in couple]

		if (len(taken_match) == 0):
			#tentatively engage the man and woman
			tentative_engagements.append([man, woman])
			free_men.remove(man)
			print('%s is no longer a free man and is now tentatively engaged to %s'%(man, woman))
			break

		elif (len(taken_match) > 0):
			print('%s is taken already..'%(woman))

			#Check ranking of the current dude and the ranking of the 'to-be' dude
			current_guy = preferred_rankings_women[woman].index(taken_match[0][0])
			potential_guy = preferred_rankings_women[woman].index(man)

			if (current_guy < potential_guy):
				print('She\'s satisfied with %s..'%(taken_match[0][0]))
			else: 
				print('%s is better than %s'%(man, taken_match[0][0]))
				print('Making %s free again.. and tentatively engaging %s and %s'%(taken_match[0][0], man, woman))
				
				#The new guy is engaged
				free_men.remove(man)

				#The old guy is now single
				free_men.append(taken_match[0][0])

				#Update the fiance of the woman (tentatively)
				taken_match[0][0] = man
				break

def stable_matching():
	'''Matching algorithm until stable match terminates'''
	while (len(free_men) > 0):
		for man in free_men:
			begin_matching(man)


def main():
	init_free_men()
	print(free_men)
	stable_matching()
	print(tentative_engagements)

main()
~~~

#### Thought

​	由于算法是男生主动追求女生，女生权衡利弊拒绝男生，这种方案实际上是对男生更有利的。每一位男生得到的伴侣都是所有可能的婚姻方案中最理想的，而女生只能在主动的人中选择。对于女生来说，如果掌握了其他人的偏好排名，也许可以通过接收不该接受或者拒绝不该拒绝的男生来实现自己的目的。因此，这个方案在实际操作中还是存在一定的难度，不过可以进行一些其他的拓展。

#### References

1[百度百科：稳定婚姻问题](https://baike.baidu.com/item/%E7%A8%B3%E5%AE%9A%E5%A9%9A%E5%A7%BB%E9%97%AE%E9%A2%98/12760040?fr=aladdin)

2.[Github:Schachte/stable-matching-algorithm](https://github.com/Schachte/stable-matching-algorithm/blob/master/stable_matching.py)

3.[“媒人”已上天堂：诺奖经济学家夏普利和他的匹配理论(组图)](http://business.sohu.com/20160315/n440476328.shtml)


  