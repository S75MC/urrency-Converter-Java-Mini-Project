\documentclass[a4paper,12pt]{article}
\usepackage[utf8]{inputenc}
\usepackage{amsmath}
\usepackage{graphicx}
\usepackage{hyperref}
\usepackage{listings}
\usepackage{xcolor}
\usepackage{tikz}
\usetikzlibrary{positioning}

\title{System Architecture for Currency Converter Application}
\author{}

\lstset{
    backgroundcolor=\color{white},
    basicstyle=\footnotesize,
    breaklines=true,
    frame=single,
    keywordstyle=\color{blue},
    commentstyle=\color{green},
    stringstyle=\color{red},
}

\begin{document}

\maketitle
\newpage

\tableofcontents
\newpage

\section{System Architecture}
\subsection{High-Level Design}
The system consists of several key components, each playing a specific role in the application workflow:

\begin{itemize}
    \item \textbf{Presentation Layer}: 
    \begin{itemize}
        \item Contains the Graphical User Interface (GUI) where the user interacts with the system.
        \item Key files include:
        \begin{itemize}
            \item \texttt{MainWindow.java}: The main application window where the user inputs data for currency conversion.
            \item \texttt{AboutWindow.java}: A dialog window that provides information about the application.
        \end{itemize}
    \end{itemize}
    
    \item \textbf{Business Logic Layer}: 
    \begin{itemize}
        \item Contains the core logic for currency conversion.
        \item Key files include:
        \begin{itemize}
            \item \texttt{CurrencyConverter.java}: Manages the main conversion logic (e.g., calculations, handling currency data).
            \item \texttt{Currency.java}: Represents a currency object with properties such as currency code, name, and exchange rates.
        \end{itemize}
    \end{itemize}
    
    \item \textbf{Utilities and Helpers}: 
    \begin{itemize}
        \item \texttt{JTextFieldLimit.java}: A helper class to limit the number of characters allowed in text fields, ensuring valid input.
    \end{itemize}
    
    \item \textbf{Localization}: 
    \begin{itemize}
        \item The localization folder contains multiple translation files (\texttt{.properties}) for supporting multilingual text (e.g., English and French). These files enable the application to switch between languages based on user settings.
    \end{itemize}
\end{itemize}

\newpage
\subsection{structure of the software system}

\begin{tikzpicture}[
  box/.style={rectangle, draw, rounded corners, minimum height=2cm, minimum width=2.8cm, align=center},
  arrow/.style={->, thick}
]

% Nodes
\node[box] (mainWindow) {MainWindow (GUI)};
\node[box, below=2cm of mainWindow] (currencyConverter) {CurrencyConverter (Logic)};
\node[box, below=2cm of currencyConverter] (currency) {Currency (Data Model)};
\node[box, right=1cm of mainWindow] (aboutWindow) {AboutWindow (GUI)};
\node[box, above=2cm of mainWindow] (localization) {Localization (Resources)};
\node[box, left=1cm of mainWindow] (textFieldLimit) {JTextFieldLimit (Utility)};

% Arrows
\draw[arrow] (mainWindow) -- (currencyConverter);
\draw[arrow] (currencyConverter) -- (currency);
\draw[arrow] (mainWindow) -- (aboutWindow);
\draw[arrow] (aboutWindow) -- (localization);
\draw[arrow] (mainWindow) -- (localization);
\draw[arrow] (mainWindow) -- (textFieldLimit);

\end{tikzpicture}

\newpage
\section{Core Components \& Modules}

\subsection{MainWindow.java (Main Window)}
Represents the main window for user interaction. This is the primary interface where users enter amounts and currencies, and the results of conversions are displayed.

\begin{lstlisting}[language=Java]
public class MainWindow extends JFrame {
    // Class contents
}
\end{lstlisting}

\subsection{AboutWindow.java (About Window)}
A simple window that displays information about the application, such as version, developers, and potentially support or contact details.
\begin{lstlisting}[language=Java]
public class AboutWindow extends JFrame {
    // Class contents
}
\end{lstlisting}

\subsection{CurrencyConverter.java}
Handles the primary logic for converting currencies based on exchange rates. It might involve fetching data from APIs or relying on predefined rates.
\begin{lstlisting}[language=Java]
public class CurrencyConverter {
    public static void main(String[] args) {
        // Entry point of the application
    }
}
\end{lstlisting}

\subsection{Currency.java}
Represents a currency object with essential attributes (e.g., name, code, and exchange rate) and is used in the conversion calculations.
\begin{lstlisting}[language=Java]
public class Currency {
    // Class contents
}
\end{lstlisting}

\subsection{JTextFieldLimit.java}
This utility class restricts the number of characters in text fields to ensure proper user input (e.g., preventing users from entering excessively large numbers or invalid characters).
\begin{lstlisting}[language=Java]
public class JTextFieldLimit extends PlainDocument {
    // Class contents
}
\end{lstlisting}


\section{Example Code Snippet}
Here’s an example of how the conversion logic might look in \texttt{CurrencyConverter.java}:

\begin{lstlisting}[language=Java, caption={CurrencyConverter.java}]
public class CurrencyConverter {
    public double convert(Currency fromCurrency, Currency toCurrency, double amount) {
        double rate = fromCurrency.getRate() / toCurrency.getRate();
        return amount * rate;
    }
}
\end{lstlisting}

\section{Interaction Between Components}
\begin{itemize}
    \item \texttt{MainWindow} interacts with \texttt{CurrencyConverter} to provide a smooth user experience, allowing users to input the amount and select the currencies for conversion.
    \item \texttt{CurrencyConverter} takes input from \texttt{MainWindow} and uses \texttt{Currency} objects to perform the conversion.
    \item \texttt{AboutWindow} is triggered from \texttt{MainWindow} when the user requests information about the app.
    \item \texttt{JTextFieldLimit} is used to ensure valid data entry in the GUI, such as restricting the number of characters in input fields.
\end{itemize}






\end{document}
