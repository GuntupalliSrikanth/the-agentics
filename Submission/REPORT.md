CrewAI Build Report

Name: Srikanth Guntupalli
Topic I used: Sanatana Dharma

1. What I changed

For my second run, I changed the Writer agent in main.py so that it was better suited to my topic, Sanatana Dharma. In the original version, the agent was a general “Technical Writer” whose purpose was to turn technical material into clear and jargon-free language. I changed its role to “Religion and Philosophy Writer” and updated its goal and backstory. The new instructions tell the Writer to explain religious and philosophical concepts carefully, distinguish historical or scriptural claims from later interpretations, and acknowledge differences in interpretation when relevant.

I also modified the writing_task so that the output would include historical and philosophical context and distinguish beliefs and interpretations from verifiable historical claims. I chose this change because Sanatana Dharma is a religious and philosophical topic, so I wanted to see whether a domain-specific Writer would produce a more focused and nuanced explanation than the original general-purpose Writer.

2. How CrewAI works

CrewAI organizes this workflow using agents, tasks, and a crew. An agent represents a role with its own goal and backstory. In this starter kit, there are three agents: a Research Analyst, a Writer, and an Editor. Each agent is assigned a task that defines what it needs to accomplish and what kind of output is expected.

The Research Analyst works first and produces a research brief containing key facts and open questions about the topic. The Writer receives the previous work as context and turns it into an explainer. Finally, the Editor reviews the explainer, tightens the writing, and marks unsupported claims with [source needed]. The Crew connects these agents and tasks using Process.sequential, so the tasks execute in order and the output from one stage becomes useful context for the next.

My change affected the Writer stage without changing the overall three-agent workflow. By changing the Writer’s role, goal, backstory, and task instructions, I gave the model more specific guidance about how to approach Sanatana Dharma. This caused the second run to focus more directly on historical context, philosophical schools, and differences in interpretation.

3. Evidence

I used the same prompt, “tell me something about sanathana dharma,” for both runs so that I could compare the results fairly. The original terminal execution is saved in run1_original.txt, and its final output is saved in explainer_run1.md. The modified execution is saved in run2_changed.txt, and its final output is in explainer_run2.md.

There is a noticeable difference between the outputs. The first run gives a broad overview organized around topics such as the four purusharthas, the range of scriptures, historical influence, and contemporary usage. The second run is more focused on historical and philosophical distinctions. For example, it discusses Advaita Vedanta and Dvaita Vedanta as different interpretations of ultimate reality and explicitly discusses the difference between historical usage and modern interpretations. The Editor also marked many of these claims with [source needed].

One thing that went wrong during the second run was that the Religion and Philosophy Writer initially returned an empty response. CrewAI displayed the error Invalid response from LLM call - None or empty twice. However, the process retried and eventually generated the Writer output successfully, after which the Editor completed its task and the crew produced the final output.

4. Choosing a framework

I would choose CrewAI for a project like this because the work can be divided naturally between specialized roles. Instead of asking one model to research, write, and review everything in one step, CrewAI lets me assign those responsibilities to separate agents. This also makes it easy to experiment with behavior. In this assignment, I was able to specialize only the Writer while keeping the Research Analyst and Editor unchanged.

Compared with LangGraph, CrewAI seems easier for a straightforward workflow where agents perform clearly defined jobs in sequence. The concepts of an agent, task, and crew closely match the idea of having a research team where each member has a responsibility. LangGraph would be useful if I needed more complicated control over the workflow, such as conditional branches, loops, retries based on custom conditions, or different paths depending on previous results. That additional control could be valuable for a larger system, but it would also require more workflow design. For this research-to-writing-to-editing process, CrewAI provided a simpler way to define specialized roles and observe how changing one role affected the final result.

5. Verification and AI use

I verified the behavior by running both versions with the same topic and comparing explainer_run1.md with explainer_run2.md. I checked whether the second output reflected the new Religion and Philosophy Writer instructions. I specifically looked for more attention to historical context, philosophical interpretations, and distinctions between different types of claims. I also checked the terminal logs to confirm that all three agents eventually completed their tasks and that the final output was written successfully.

I did not treat the factual claims in the generated explainers as automatically verified. The starter kit has no web access, and the Editor itself marked many statements with [source needed]. Therefore, those statements would need external sources before being used as verified factual information.

I used ChatGPT as AI assistance to understand the assignment, choose a meaningful modification, modify the Writer agent and writing task, and help prepare this report. I verified the suggested code change by running it myself and reviewing the actual terminal output and generated explainer rather than assuming that the AI-generated modification worked correctly.