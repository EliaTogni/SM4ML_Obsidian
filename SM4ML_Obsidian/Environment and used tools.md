Prior to delving into the intricacies of different theoretical frameworks and implementation decisions, this section introduces the primary tools and environment utilized for running the developed code. These choices, in my assessment, are pertinent for executing the models and setting up experiments effectively.

The whole code has been written in a Google Colab environment, which provides Jupyter-notebook, a free notebook for Python$3$-code execution. I chose this environment because of its simplicity and intuitiveness, which made easier to code with multiple libraries.

Here we present a brief list of the main packages and libraries used:
\begin{itemize}
\item Pillow
\item
\item
\item
\end{itemize}

For the sake of the replicability of the experiments, I listed below a detailed list of the version of the used software, libraries and programming languages.



\caption{Versions of the used software, libraries and programming languages}
\end{table}

#### Questa parte con colab non dovrebbe più servire 
In Linux, the \textit{ulimit} command is used to control and limit the resources available to user processes. This command is useful for managing system resources to avoid excessive or inefficient resource usage.
The `ulimit` command can be used to control different types of resources, including limiting the number of open files. This parameter controls the maximum number of files a process can open simultaneously. For this reason, I had to use the command \textit{ulimit -n 8000}.

----------------------------------------------------------------