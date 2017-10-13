/**
 * 
 */
package com.expedia.web.filter;

import java.io.IOException;
import java.util.Iterator;
import java.util.Map;
import java.util.Set;
import java.util.Map.Entry;

import javax.servlet.Filter;
import javax.servlet.FilterChain;
import javax.servlet.FilterConfig;
import javax.servlet.ServletException;
import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;

import org.apache.commons.lang.StringEscapeUtils;
import org.apache.log4j.Logger;

/**
 * This filter is responsible of filtering all incoming input text by
 * running HTML escape method on it to prevent possible vulnerabilities
 * 
 * @author Hala Odeh
 * @since Oct 13, 2017
 */
public class InputFilter implements Filter {
    private final static Logger logger = Logger.getLogger("InputFilter");

    /**
     * @see javax.servlet.Filter#destroy()
     */
    @Override
    public void destroy() {
        // TODO Auto-generated method stub
    }

    /**
     * @see javax.servlet.Filter#doFilter(javax.servlet.ServletRequest, javax.servlet.ServletResponse, javax.servlet.FilterChain)
     */
    @Override
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException,
    ServletException {

        Map parameterMap = request.getParameterMap();
        Set keys = parameterMap.entrySet();
        Entry entry = null;
        Iterator iterator = keys.iterator();

        while (iterator.hasNext()) {
            entry = (Entry) iterator.next();
            clean((String[]) entry.getValue());
            request.getParameterMap().put(entry.getKey(), entry.getValue());
        }

        chain.doFilter(request, response);
    }

    /**
     * @see javax.servlet.Filter#init(javax.servlet.FilterConfig)
     */
    @Override
    public void init(FilterConfig filterConfig) throws ServletException {
        // TODO Auto-generated method stub
    }

    /**
     * cleaning any value in the passed array
     * 
     * @param parameter array of values to be escaped
     */
    private void clean(String[] parameter) {
        try {
            int length = parameter.length;

            for (int i = 0; i < length; i++) {
                String escaped = StringEscapeUtils.escapeHtml(parameter[i]);
                if (!escaped.contains("&#")) {
                    parameter[i] = escaped;
                }
            }
        } catch (Exception e) {
            logger.error("Exception while escaping parameters", e);
            return;
        }
    }

}
