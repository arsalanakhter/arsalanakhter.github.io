---
title:  "Exploring Asprilo"
date:   2020-05-17 15:16:00
categories: [Warehouse Robotics]
tags: [Multi-agent, Path Finding, MAPF, Warehouse, Robotics, Multi-robot, Simulator, Asprilo]
---

Asprilo is an open-source simulator for simulating robots in a warehouse environemnt, much like amazon robotics style robots. The goal of this post is to see how can we quickly get asprilo up and running.

From [asprilo's website](https://asprilo.github.io/):

<p style="text-align: center;">
<em>
<strong>asprilo</strong> is a benchmarking framework to study typical scenarios in intra-logistics and warehouse automation with multiple mobile robots.
</em>
</p>

Following video shows an instance of the software, with detailed installation instructions [here](https://asprilo.github.io/visualizer/). 

<iframe width="640" height="360" src="https://www.youtube.com/embed/ifYKHIvdnjw" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


<h3>Quick Setup</h3>


We'll jump right into getting it up and running. Assuming we have [anaconda installed](https://conda.io/projects/conda/en/latest/user-guide/install/index.html), (which is an environment manager for python), we can run the following commands to get it up and running.

```bash
$ conda create -n asprilo-env python=3.6
$ conda activate asprilo-env
$ conda config --add channels potassco
$ conda config --add channels potassco/label/dev
$ conda install -y asprilo-visualizer asprilo-generator
```

To confirm if everything is installed correctly, type 
```bash
$ gen -h
```
which should result in a help output for aspirilo generator.

Documentation on Aspirilo Generator can be found [here](https://asprilo.github.io/generator/). We'll create a new instance using the following command

```bash
$ mkdir asprilo-ws && cd asprilo-ws
$ gen -x 13 -y 12 -X 5 -Y 2 -s 30 -p 3 -r 5 -H -P 6 -u 32 -o 8 --spr 2 -t 4
```
Where we generate an instance with

- 13 x 12 grid `x 13 -y 12`
- 5 x 2 shelf cluster dimensions `-X 5 -Y 2`
- 30 shelves `-s 30`
- 3 picking stations `-p 3`
- 5 robots `-r 5`
- highway-layout `-H`
- 6 products `-P 6`
- 32 product units `-u 32`
- 8 orders `-o 8`
- 3 shelves per product that hold its units `--spr 3`
- 4 clingo threads `-t 4`

This will generate a new instance in a new folder named `generatedInstances`.

To visualize the result, we can run 

```bash
$  viz -l generatedInstances/x13_y12_n156_r5_s30_ps3_pr6_u32_o8_l8_N001.lp
```
which opens the visulizer with the generated result, as follows:

![Generated Result in Aspirilo]({{site.baseurl}}/images/asprilo/asprilo1.jpeg)

Concluding, aspirilo is a useful tool to simulate warehouse robots. Here we just looked at how to quickly get the simulation environment up and running for a warehouse robotics scenario. 

In a future post we may further explore how to actually plan paths for these robots.





